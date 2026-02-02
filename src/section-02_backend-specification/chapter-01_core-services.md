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
POST   /auth/register
POST   /auth/login
POST   /auth/logout
POST   /auth/refresh
GET    /auth/profile
PUT    /auth/profile
PUT    /auth/credentials
```

### User management

- **Purpose**: User profile management and user-related operations
- **Database**: Users collection
- **File storage**: MinIO avatars bucket
- **Dependencies**: Authorization, MongoDB, MinIO
- **Tech Stack**: Go, Gin framework, MongoDB driver, MinIO SDK

**Responsibilities**:

- User profile CRUD operations
- Avatar and media upload
- User preferences management
- User search and discovery

**Key Endpoints**:

```
GET    /users/{id}
PUT    /users/{id}
GET    /users/search
POST   /users/{id}/avatar
PUT    /users/{id}/preferences
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
GET    /organizations
POST   /organizations
GET    /organizations/{id}
PUT    /organizations/{id}
DELETE /organizations/{id}
POST   /organizations/{id}/members
PUT    /organizations/{id}/members/{userId}
DELETE /organizations/{id}/members/{userId}
POST   /organizations/{id}/logo
```

### Team management

- **Purpose**: Team management and roster operations
- **Database**: Teams collection
- **Dependencies**: Authentication Service, Organization Service, MongoDB, MinIO

**Responsibilities**:

- Team CRUD operations
- Roster management
- Team achievements tracking
- Team branding
- Team search and discovery

**Key Endpoints**:
```
GET    /teams
POST   /teams
GET    /teams/{id}
PUT    /teams/{id}
DELETE /teams/{id}
POST   /teams/{id}/roster
PUT    /teams/{id}/roster/{userId}
DELETE /teams/{id}/roster/{userId}
POST   /teams/{id}/achievements
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

**Key Endpoints**:

```
GET    /tournaments
POST   /tournaments
GET    /tournaments/{id}
PUT    /tournaments/{id}
DELETE /tournaments/{id}
POST   /tournaments/{id}/register
GET    /tournaments/{id}/registrations
PUT    /tournaments/{id}/registrations/{regId}
POST   /tournaments/{id}/generate-bracket
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

**Key Endpoints**:

```
GET    /matches
GET    /matches/{id}
PUT    /matches/{id}/schedule
POST   /matches/{id}/result
PUT    /matches/{id}/result
POST   /matches/{id}/evidence
GET    /tournaments/{tournamentId}/matches
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

**Key Endpoints**:

```
POST   /upload/image
POST   /upload/video
GET    /files/{id}
DELETE /files/{id}
```

### API Gateway

- **Purpose**: Request routing, rate limiting, and API aggregation
- **Dependencies**: All services

**Responsibilities**:

- Request routing and load balancing
- Rate limiting and throttling
- API key management
- Request/response logging
- CORS handling


