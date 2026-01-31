# API Specification

Tournabyte implements an API architecture following RESTful principles. An upper level gateway will route requests to their appropriate domain routing groups. The flutter front end component is expected to communicate with this API using JSON request/response patterns.

A generic response from this API follows the pattern shown below

```JSON
{
  "ok": "bool" // true if the request was fulfilled successfully, otherwise false
  "data" : {...}, // the data corresponding to the fulfilled request (present if ok is true)
  "error": {
    "message": "string",
    "details": {...} // Can be null if no details to give
  } // specific error information corresponding to the issue preventing the request's fulfillment (present if ok is false)
}
```

## Authentication/authorization endpoints

### Create user

**Request**

```plaintext
POST /v1/auth/register
Content-Type: application/json

{
  "email": "string",
  "password": "string",
  "displayName": "string",
}
```

**OK response**

```plaintext
Response 201:
{
  "ok": true,
  "data": {
    "user": {
      "id": "string",
      "email": "string",
      "displayName": "string",
    },
    "accessToken": "JWT token",
    "refreshToken": "Refresh token"
  }
}
```

### User login

**Request**

```http
POST /v1/auth/login
Content-Type: application/json

{
  "email": "string",
  "password": "string"
}
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "user": {
      "id": "string",
      "displayName": "string",
      "avatarUrl": "string|null",
    },
    "accessToken": "JWT token",
    "refreshToken": "Refresh token"
  }
}
```

**Not OK response**

```http
Error Response 401:
{
  "ok": false,
  "error": {
    "message": "Invalid email or password"
  }
}
```

### Token refresh

**Request**

```http
POST /v1/auth/refresh
Authorization: Bearer <refreshToken> 
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "accessToken": "new JWT",
    "refreshToken": "new refresh token"
  }
}
```

**Not OK response**

```http
Response 403:
{
  "ok": false,
  "error": {
    "message": "Invalid refresh token provided. All active sessions revoked"
  }
}
```

### Profile management

#### Retrieving a profile

**Request**

```http
GET /v1/auth/profile
Authorization: Bearer <token>
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "id": "string",
    "email": "string",
    "displayName": "string",
    "avatarUrl": "string",
    "bio": "string", 
    "preferences": {
      "language": "en",
      "timezone": "UTC",
    },
    "createdAt": "ISO8601",
    "updatedAt": "ISO8601"
  }
}
```

**Not OK response**

```http
Response 401:
{
  "ok": false,
  "error": {
    "message": "access denied",
    "details": {
      "reason": "presented token has insufficient claim to the requested resource",
      "resolve": "refresh access token and try again"
    }
  }
}
```

#### Updating a profile

**Request**

```http
PUT /v1/auth/profile
Authorization: Bearer <token>

{
  "displayName": "new displayName",
  "bio": "new bio",
  "preferences": {
    "language": "new language preference",
    "timezone": "new timezone preference"
  }
}
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "id": "string",
    "email": "string",
    "displayName": "string",
    "avatarUrl": "string",
    "bio": "string", 
    "preferences": {
      "language": "en",
      "timezone": "UTC",
    },
    "createdAt": "ISO8601",
    "updatedAt": "ISO8601"
  }
}
```

**Not OK response**

```http
Response 401:
{
  "ok": false,
  "error": {
    "message": "access denied",
    "details": {
      "reason": "presented token has insufficient claim to the requested resource",
      "resolve": "refresh access token and try again"
    }
  }
}
```

```http
Response 400:
{
  "ok": false,
  "error": {
    "message": "field `{}` is not modifiable"
    "details": {
      "field": "bad field",
      "reason": "not modifiable|not recognized"
    }
  }
}
```

### Credential management

**Request**

```http
PUT /v1/auth/credentials
{
  "email": "new email",
  "password": "new password"
}
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "email": "updated successfully",
    "password": "updated successfully"
  }
}
```

**Not OK response**

```http
Response 400
{
  "ok": false,
  "error": {
    "message": "credentials were not modified"
    "details": {
      "email": "invalid format",
      "password": "security requirements not met"
    }
  }
}
```

## Organization endpoints

### Create organization

**Request**

```http
POST /v1/organizations
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "string",
  "description": "string",
  "contactEmail": "string",
  "website": "string",
  "socialLinks": {
    "twitter": "string",
    "discord": "string",
    "twitch": "string",
    "youtube": "string"
  }
}
```

**OK response**

```http
Response 201:
{
  "ok": true,
  "data": {
    "id": "string",
    "name": "string",
    "slug": "string",
    "description": "string",
    "logoUrl": "string|null",
    "bannerUrl": "string|null",
    "contactEmail": "string",
    "socialLinks": {
      "twitter": "string",
      "discord": "string",
      "twitch": "string",
      "youtube": "string"
    },
    "createdAt": "Date",
  }
}
```

**Not OK response**

```http
Response 400:
{
  "ok": false,
  "error": {
    "message": "organization not created"
  }
}
```

### List organizations

**Request**

```http
GET /v1/organizations
Authorization: Bearer <token>
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "page": [
      {
        "id": "string",
        "name": "string",
        "slug": "string",
        "description": "string",
        "logoUrl": "string|null",
        "bannerUrl": "string|null",
        "socialLinks": {
          "twitter": "string",
          "discord": "string",
          "twitch": "string",
          "youtube": "string"
        },
        "memberCount": number,
        "activeEvents": number,
        "createdAt": "ISO8601"
      },
      ...
    ],
    "pagination": {
      "offset": "integer",
      "limit": "integer"
    }
  }
}
```

**Not OK response**

```http
5XX
{
  "ok": false,
  "error": {
    "message": "string"
  }
}
```

### Find organization by ID

**Request**

```http
GET /v1/organizations/{id}
Authorization: Bearer <token>
```

**OK response**

```http
Response 200
{
  "ok": true,
  "data": {
    "id": "string",
    "name": "string",
    "slug": "string",
    "description": "string",
    "logoUrl": "string|null",
    "bannerUrl": "string|null",
    "socialLinks": {
      "twitter": "string",
      "discord": "string",
      "twitch": "string",
      "youtube": "string"
    },
    "memberCount": number,
    "activeEvents": number,
    "createdAt": "ISO8601"
  }
}
```

**Not OK response**

```http
Response 404
{
  "ok": false,
  "error": {
    "message": "requested resource does not exist",
    "details": {
      "parameter": "id",
      "reason": "no such organization with ID: {id}"
    }
  }
}
```

### Update organization details

**Request**

```http
GET /v1/organizations/{id}
Authorization: Bearer <token>

{
  "name": "string",
  "description": "string",
  "contactEmail": "string",
  "socialLinks": {
    "twitter": "string",
    "discord": "string",
    "twitch": "string",
    "youtube": "string"
  }
}
```

**OK response**

```http
Response 200
{
  "ok": true,
  "data": {
    "id": "string",
    "name": "string",
    "slug": "string",
    "description": "string",
    "logoUrl": "string|null",
    "bannerUrl": "string|null",
    "socialLinks": {
      "twitter": "string",
      "discord": "string",
      "twitch": "string",
      "youtube": "string"
    },
    "memberCount": number,
    "activeEvents": number,
    "createdAt": "ISO8601"
  }
}
```

**Not OK response**

```http
Response 400:
{
  "ok": false,
  "error": {
    "message": "organization not updated",
    "details": {
      "<field>": "validation failed|not recognized"
    }
  }
}

Response 401:
{
  "ok": false,
  "error": {
    "reason": "presented token has insufficient claim to the requested resource",
    "resolve": "refresh access token and try again"
  }
}
```

### Delete organization

**Request**

```http
DELETE /v1/organizations/{id}
Authorization: Bearer <token>
```

**OK response**

```http
Response 200
{
  "ok": true,
  "data": {
    "organization": "organization with ID {id} successfully deleted"
  }
}
```

**Not OK response**

```http
Response 401
{
  "ok": false,
  "error": {
    "message": "access denied",
    "details": {
      "reason": "presented token has insufficient claim to the requested resource",
      "resolve": "refresh access token and try again"
  }
}
```

## Event endpoints

### Create event

**Request**

```http
POST /v1/organizations/{id}/events
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "string",
  "description": "string",
  "game": "string",
  "participantRequirements": {
    "minimumParticipants": "integer",
    "maximumParticipants": "integer",
    "participantType": "individual|team",
    "participantRegistrationOpen": bool
  },
  "schedule": {
    "startsAt": "Date",
    "endsAt": "Date"
  },
  "prize": {
    "totalAmount": "integer",
    "currency": "string (ISO4217)"
    "distribution": [
      {
        "placement": "integer",
        "amount": "integer"
      },
      ...
    ]
  }
}
```

**OK response**

```http
Response 201:
{
  "ok": true,
  "data": {
    "id": "string",
    "logo": "string|null",
    "banner": "string|null",
    "name": "string",
    "description": "string",
    "game": "string",
    "participantRequirements": {
      "minimumParticipants": "integer",
      "maximumParticipants": "integer",
      "participantType": "individual|team",
      "participantRegistrationOpen": bool
    },
    "schedule": {
      "startsAt": "Date",
      "endsAt": "Date"
    },
    "prize": {
      "totalAmount": "integer",
      "currency": "string (ISO4217)"
      "distribution": [
        {
          "placement": "integer",
          "amount": "integer"
        },
        ...
      ]
    },
    "participants": [],
    "matches": []
  }
}
```

**Not OK response**

```http
Response 400
{
  "ok": false,
  "error": {
    "message": "event was not created",
    "details": {
      "<field>": "validation failed"
    }
  }
}

Response 401
{
  "ok": false,
  "error": {
    "message": "access denied",
    "reason": "presented token has insufficient claim to the requested resource",
    "resolve": "refresh access token and try again"
  }
}
```

### Update event

**Request**

```http
PUT /v1/organizations/{id}/events
Authorization: Bearer <token>
Content-Type: application/json

{
  "name": "string",
  "description": "string",
  "game": "string",
  "participantRequirements": {
    "minimumParticipants": "integer",
    "maximumParticipants": "integer",
    "participantType": "individual|team",
    "participantRegistrationOpen": bool
  },
  "schedule": {
    "startsAt": "Date",
    "endsAt": "Date"
  },
  "prize": {
    "totalAmount": "integer",
    "currency": "string (ISO4217)"
    "distribution": [
      {
        "placement": "integer",
        "amount": "integer"
      },
      ...
    ]
  }
}
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "id": "string",
    "logo": "string|null",
    "banner": "string|null",
    "name": "string",
    "description": "string",
    "game": "string",
    "participantRequirements": {
      "minimumParticipants": "integer",
      "maximumParticipants": "integer",
      "participantType": "individual|team",
      "participantRegistrationOpen": bool
    },
    "schedule": {
      "startsAt": "Date",
      "endsAt": "Date"
    },
    "prize": {
      "totalAmount": "integer",
      "currency": "string (ISO4217)"
      "distribution": [
        {
          "placement": "integer",
          "amount": "integer"
        },
        ...
      ]
    },
    "participants": [],
    "matches": []
  }
}
```

**Not OK response**

```http
Response 400
{
  "ok": false,
  "error": {
    "message": "event was not updated",
    "details": {
      "<field>": "validation failed"
    }
  }
}

Response 401
{
  "ok": false,
  "error": {
    "message": "access denied",
    "reason": "presented token has insufficient claim to the requested resource",
    "resolve": "refresh access token and try again"
  }
}
```

### Create participant registration

**Request**

```http
POST /v1/organizations/{id}/events/{id}/registration
Authorization: Bearer <token>
Content-Type: application/json

{
  "registerAs": "string (participant/team ID)",
  "notes": "string (optional)"
}
```

**OK response**

```http
Response 201:
{
  "ok": true,
  "data": {
    "id": "string",
    "notes": "string",
    "status": "pending",
    "registeredAt": "Date"
  }
}
```

**Not OK response**

```http
Response 401
{
  "ok": false,
  "error": {
    "message": "access denied",
    "reason": "presented token has insufficient claim to the requested resource",
    "resolve": "refresh access token and try again"
  }
}

Response 400
{
  "ok": false,
  "error": {
    "message": "registration not completed",
    "details": {
      "<field>": "validation failed"
    }
  }
}
```

### Update participant registration

**Request**

```http
PUT /v1/organizations/{id}/events/{id}/registration/{id}
Authorization: Bearer <token>
Content-Type: application/json

{
  "status": "string"
  "notes": "string (optional)"
}
```

**OK response**

```http
Response 201:
{
  "ok": true,
  "data": {
    "id": "string",
    "notes": "string",
    "status": "string",
    "registeredAt": "Date"
  }
}
```

**Not OK response**

```http
Response 401
{
  "ok": false,
  "error": {
    "message": "access denied",
    "reason": "presented token has insufficient claim to the requested resource",
    "resolve": "refresh access token and try again"
  }
}

Response 400
{
  "ok": false,
  "error": {
    "message": "registration not completed",
    "details": {
      "<field>": "validation failed"
    }
  }
}
```

### Get bracket

**Request**

```http
GET /v1/organizations/{id}/events/{id}/bracket
Authorization: Bearer <token>
Content-Type: application/json
```

**OK response**

```http
{
  "ok": true,
  "data": {
    "matchgraph": "<graph>"
  }
}
```

**Not OK response**

```http
Response 404
{
  "ok": false,
  "error": {
    "message": "resource not found",
    "reason": "the bracket for event with ID {id} does not exist"
  }
}

Response 401
{
  "ok": false,
  "error": {
    "message": "access denied",
    "reason": "presented token has insufficient claim to the requested resource",
    "resolve": "refresh access token and try again"
  }
}
```

## Participant endpoints

### Add player participant

### Update player participant

### Delete player participant

### Add team participant

### Update team participant

### Delete team participant

## Match endpoints

### Update match status

### Update match schedule

### Update match result

## Supporting endpoints

### File upload

**Request**

```http
PUT /v1/files/
Authorization: Bearer <token>
Content-Type: form/data

key: string
contents: bytes
```

**OK response**

```http
Response 200
{
  "ok": true,
  "data": {
    "key": "file contents successfully uploaded"
  }
}
```

**Not OK response**

```http
Response 401
{
  "ok": false,
  "error": {
    "message": "access denied",
    "details": {
      "reason": "presented token has insufficient claim to the requested resource",
      "resolve": "refresh access token and try again"
  }
}
```

### File retrieval

**Request**

```http
GET /v1/files/?key={path}
```

**OK response**

```http
Response 200:
{
  "ok": true,
  "data": {
    "downloadLink": "string"
  }
}
```

**Not OK response**

```http
Response 404
{
  "ok": false,
  "error": {
    "message": "requested resource not found",
    "details": {
      "path": "no file associated with this key"
    }
  }
}
```
