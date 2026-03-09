# Core Services

## Service Components

### Authentication

- **Purpose**: User authentication, authorization, and session management
- **Database**: Users collection
- **Dependencies**: MongoDB
- **Tech Stack**: Go, Gin framework, JWT library, password hashing library

**Responsibilities**:
- User registration and login
- JWT token generation and validation
- Password hashing and verification
- Session management
- Role-based access control


**Key Endpoints**:

```
POST   /auth/register     --create user
POST   /auth/login        --create session
DELETE /auth/login        --revoke session
POST   /auth/refresh      --renew session
PUT    /auth/credentials  --change password
```

### Organization management

- **Purpose**: Managing and administering of organizations
- **Database**: Organizations collection
- **File storage**: MinIO organization assets bucket
- **Dependencies**: Authorization, MongoDB, MinIO
- **Tech Stack**: Go, Gin framework, MongoDB driver, MinIO SDK

**Responsibilities**:

- Organization CRUD operations
- Member management and role assignment
- Organization settings and branding
- Public organization profiles
- Organization search

**Key Endpoints**:

```
GET    /organizations                         --get page of organization (query parameter filters)
POST   /organizations                         --create an organization
GET    /organizations/{id}                    --get a specific organization
PUT    /organizations/{id}                    --update a specific organization
DELETE /organizations/{id}                    --remove an organization
POST   /organizations/{id}/members            --add a member to the organization
GET    /organizations/{id}/members/{id}       --retrieve an organization members data (could be team or player)
PUT    /organizations/{id}/members/{id}       --update an organization member (could be team or player)
DELETE /organizations/{id}/members/{id}       --remove a member from the organization
PUT    /organizations/{id}/logo               --set a specific organization's logo image
PUT    /organizations/{id}/banner             --set a specific organization's banner image
PUT    /organizations/{id}/social             --set a social link key:value pair
DELETE /organizations/{id}/social             --remove a social link key:value pair
```

### Membership management

- **Purpose**: management of sub-resources of organization member (players and teams)
- **Database**: Membership collection (sub-collections of either type `player` or `team`)
- **Dependencies**: Authentication Service, Organization Service, MongoDB, MinIO

**Responsibilities**:

- Team CRUD operations
- Roster management
- Team achievements tracking
- Team branding
- Team search and discovery
- Player profile CRUD operations
- Avatar and media upload
- Player preferences management
- Player search and discovery

**Key Endpoints** (assumed prefix of `/organizations/{id}/members/{id}/`):

```
-- Team specific
PUT    %PREFIX%/roster/          --add a player to a roster (must be in same organization)
GET    %PREFIX%/roster/{id}      --view a roster member's profile (this is a player and players should update their own profiles)
DELETE %PREFIX%/roster/{id}      --remove a player from a roster
POST   %PREFIX%/achievements     --award an achievement to a team
GET    %PREFIX%/achievements     --list team achievements
GET    %PREFIX%/logo             --get a team's logo image
PUT    %PREFIX%/logo             --set a team's logo image
GET    %PREFIX%/banner           --get a team's banner image
PUT    %PREFIX%/banner           --set a team's banner image
-- Player specific
GET    %PREFIX%/avatar           --get a player's avatar image
PUT    %PREFIX%/avatar           --set a player's avatar image
GET    %PREFIX%/preferences      --get a player's preferences
PUT    %PREFIX%/preferences      --set a player's preferences
PUT    %PREFIX%/social           --set a social link key:value pair
DELETE %PREFIX%/social      --remove a social link key:value pair
```

### Event management

- **Purpose**: Event creation, management, and coordination
- **Database**: Event collection
- **Dependencies**: Authentication, Organization, MongoDB, MinIO

**Responsibilities**:

- Tournament CRUD operations
- Registration management
- Bracket generation
- Tournament settings and rules
- Tournament search and filtering

**Key Endpoints** (assumed prefix of `/organizations/{id}/`):

```
GET    %PREFIX%/events                                   --list an organizations events
POST   %PREFIX%/events                                   --create a new event
GET    %PREFIX%/events/{id}                              --get a specific event
PUT    %PREFIX%/events/{id}                              --update a specific event
DELETE %PREFIX%/events/{id}                              --remove a specific event
GET    %PREFIX%/events/{id}/logo                         --get an event's logo image
PUT    %PREFIX%/events/{id}/logo                         --set an event's logo image
GET    %PREFIX%/events/{id}/banner                       --get a event's banner image
PUT    %PREFIX%/events/{id}/banner                       --set a event's banner image
GET    %PREFIX%/events/{id}/registrations                --get an event's registration requirements
PUT    %PREFIX%/events/{id}/registrations                --set an event's registration requirements
GET    %PREFIX%/events/{id}/schedule                     --get an event's schedule information
PUT    %PREFIX%/events/{id}/schedule                     --set an event's schedule information
GET    %PREFIX%/events/{id}/prize                        --get an event's prize pool information
PUT    %PREFIX%/events/{id}/prize                        --set an event's prize pool information
PUT    %PREFIX%/events/{id}/participants                 --add a team/player participant
DELETE %PREFIX%/events/{id}/participants/{id}            --remove a team/player from the participants list
POST   %PREFIX%/events/{id}/bracket                      --generate the event bracket (replaced if already existing)
GET    %PREFIX%/events/{id}/bracket                      --get the current event bracket
```

### Matchmaking

- **Purpose**: Match scheduling, coordination, and result management
- **Database**: Matches collection
- **File storage**: MinIO evidence bucket
- **Dependencies**: Event Service, Authorization, MongoDB, MinIO

**Responsibilities**:

- Match scheduling
- Result reporting and validation
- Match evidence management
- Match status updates
- Score tracking

**Key Endpoints** (assumed prefix of `/organizations/{id}/events/{id}`):

```
PUT    %PREFIX%/matches/{id}/schedule            --set a match's schedule
GET    %PREFIX%/matches/{id}/schedule            --get a match's schedule
PUT    %PREFIX%/matches/{id}/result              --set a match's result
GET    %PREFIX%/matches/{id}/result              --get a match's result
GET    %PREFIX%/matches/{id}/participants        --get a match's participant pair
```

## Supporting services

### File Upload Service

- **Purpose**: Binary file handling and storage coordination
- **Dependencies**: MinIO, MongoDB

**Responsibilities**:

- File upload validation
- Image processing and resizing
- File metadata storage
- CDN URL generation
- File access control

### API Gateway

- **Purpose**: Request routing, rate limiting, and API aggregation
- **Dependencies**: All services

**Responsibilities**:

- Request routing and load balancing
- Rate limiting and throttling
- API key management
- Request/response logging
- CORS handling


