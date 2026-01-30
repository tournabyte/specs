# Data models

## Mongo DB Document Structures

The following code snippets illustrate the anticipated structure of the documents stored within Mongo DB. As the database support flexible schemas, fields can be added or removed as needed

### User accounts

Documents of this type represent a user account on the Tournabyte platform. The documents are expected to be stored under a `accounts` collection within a `tournabyte` database.

```json
{
  "_id": "ObjectId",
  "email": "string (unique, required)", // Used for login
  "passwordHash": "string (required)",
  "displayName": "string (required)", // Used for public profiles
  "avatarKey": "string (MinIO Key, optional)",
  "bio": "string (optional)",
  "preferences": {
    "language": "string (default: 'en')",
    "timezone": "string (default: 'UTC')",
  },
  "createdAt": "Date (auto)",
  "updatedAt": "Date (auto)",
}
```

### Organizations

Documents of this type represent an organized community on the Tournabyte platform. The documents are expected to be stored under a `organizations` collection within a `tournabyte` database.

```json
{
  "_id": "ObjectId",
  "name": "string (required)",
  "slug": "string (unique, required)",
  "description": "string (optional)",
  "logoKey": "string (MinIO Key, optional)",
  "bannerKey": "string (MinIO Key, optional)",
  "contactEmail": "string (required)", //Defaults to owner's email, but can be changed
  "socialLinks": { // Omitted if empty
    "twitter": "string",
    "discord": "string",
    "twitch": "string",
    "youtube": "string"
  },
  "createdAt": "Date (auto)",
  "updatedAt": "Date (auto)",
  "members": [
    {
      "user": "ObjectId" // References an account's "_id" field. Creator is automatically part of this list
      "role": "string oneof(admin, staff, participant, spectator)"
      "joinedAt": "Date (auto)"
    },
  ],
  "teams": [
    {
      "team": "ObjectId" // References a team's "_id" field.
      "role": "string (default to participant)",
      "joinedAt": "Date (auto)"
    }
  ],
  "events": [
    "ObjectId" // References an event's "_id" field
  ]
}
```

### Teams

Documents of this type represent an organized group of players intending to participate in an organization's team events. The documents are expected to be stored under a `teams` collection within a `tournabyte` database.

```json
{
  "_id": "ObjectId",
  "name": "string (required)",
  "slug": "string (required)",
  "discription": "string (optional)",
  "logoKey": "string (MinIO Key, optional)",
  "bannerKey": "string (MinIO Key, optional)",
  "roster": [
    {
      "user": "ObjectId", // References an account's "_id" field. Captain is automatically part of this list
      "role": "string oneof(captain, starter, bench)",
      "joinedAt": "Date (auto)"
    }
  ],
  "achievements": [
    {
      "event": "ObjectId", // References an event's "_id" field.
      "placement": "integer",
      "achievedAt": "Date (auto)"
    }
  ],
  "createdAt": "Date (auto)",
  "updatedAt": "Date (auto)"
}
```

### Events

Documents of this type represent an e-sports event organized and run by an organization. The documents are expected to be stored under an `events` collection within a `tournabyte` database

```json
{
  "id": "ObjectId",
  "name": "string (required)",
  "slug": "string (required)",
  "description": "string (optional)",
  "logoKey": "string (MinIO Key, optional)",
  "bannerKey": "string (MinIO Key, optional)",
  "game": "string (required)",
  "participantRequirements": {
    "minimumParticipants": "integer",
    "maximumParticipants": "integer",
    "participantType": "string oneof(team, user)"
    "participantRegistrationOpen": "bool"
  },
  "participants": [
    {
      "participantID": "ObjectId" // Reference to an account's or a team's "_id" field,
      "registeredAt": "Date (auto)",
      "status": "string oneof(pending, approved, rejected, waitlisted)",
      "approvedAt": "Date (auto)",
      "approvedBy": "ObjectId", //Reference to an account's "_id" field
      "notes": "string (optional)"
    },
    ... // One for each submitted registration
    // Actual participants are the first ${maximumParticipants} approved ordered by approval time
  ],
  "eventSchedule": {
    "startsAt": "Date (auto)",
    "endsAt": "Date (auto)"
  },
  "eventPrizePool": {
    "totalAmount": "integer (required)",
    "currency": "string (ISO 4217)",
    "distribution": [ //At least one required if prize pool specified
      {
        "placement": "integer",
        "amount": "integer"
      },
      ...
    ] // Sum of amounts should equal totalAmount
  },
  "matches": [
    "ObjectId" // References a match's "_id" field
  ],
  "createdAt": "Date (auto)",
  "updatedAt": "Date (auto)"
}
```

### Matches

Documents of this type represent a match between participants in an organization's event. The documents are expected to be stored in a `matches` collection within a `tournabyte` database

```json
{
  "id": "ObjectId",
  "status": "string oneof(scheduled, in-progress, completed, disputed, cancelled)",
  "participants": [
    {
      "source": "string oneof(seed, match)" // Seed is a starting position in a event, match is a previous match in a event
      // The following two fields should be mutually exclusive (one or the other exists, but not both)
      "seed": "integer" // Seed position of participant
      "match": "ObjectId" // Reference to previous round match up (refers to another match "_id" field)

      "participantID": "ObjectId" // References an account or team "_id" field
    }
  ],
  "schedule": {
    "startsAt": "Time (auto)",
    "estimatedDuration": "integer (in minutes)",
    "streamURLs": { // Omit if empty
      "twitch": "string",
      "youtube": "string",
      ...
    }
  },
  "result": {
    "winner": "ObjectId", // References the "_id" field from one of the participant
    "completedAt": "Time (auto)",
    "reportedBy": "ObjectId" // References an account's "_id" field
    "finalScores": {
      "game 1": {
        "ObjectId": "integer",
        ... // One for each participant
      },
      ... // One for each game played
    },
    "evidence": [
      {
        "evidenceKey": "string (MinIO Key, optional)",
        "evidenceDescription": "string (optional)"
      },
    ]
  },
  "createdAt": "Date (auto)",
  "updatedAt": "Date (auto)"
}
```

## Document Relationships

### Account relationships

**Account m<->n Organizations**

- An account can belong to many organizations
- An organization can have many accounts as members

**Account m<->n Team**

- An account can be part of multiple teams
- A team consists of multiple accounts

**Account m<->n Event**

- An account can participate directly in an event if the `participantType` is user
- Accounts can participate indirectly as
  - Registrants
  - Approvers
  - Reporters of match data

**Account 1<->n Match**

- An account can
  - Report match results
  - participate in a match (if `participantType` is user)

### Organization relationships

**Organization 1<->m Team**

- An organization can host multiple teams
- An team can belong to one organization

**Organization 1<->m Event**

- An organization runs many events (hopefully)
- Events belong to the organization that runs them

**Organization 1<->m Account**

- The creator/admin of an organization is an account
- Ownership implied by initial membership
- An organization can consist of many admin/staff/participant accounts

### Team relationships

**Team n<->m Event**

- A team can play in many events
- An event can have many competing teams

**Team n<->m Match**

- A team can play in many matches
- A match can have many participating teams (typically 2)

**Team 1<->m Achievement**

- A team can have many achievements (if they don't suck)
- Each achievement belong to a single team

### Event relationships

**Event 1<->m Match**

- An event contains many matches
- Each match belongs to a single event

**Event n<->m Participant (account or team)**

- Participants can be either a user or team (depending on `participantType` of the event)
- Participants can participate in multiple events
- Events have many participants

### Match relationships

**Match <-> Match**

- Represents a directed graph structure
- A match can depend on the result of previous matches
- Used to model tournament brackets
