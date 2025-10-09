# Backlog Refinement - 2025-10-09

## Items Discussed
<!-- Items currently in the backlog that were discussed in this meeting -->
> No current items discussed

## Newly Identified Items
<!-- Items that were added to the backlog during this meeting -->
| title | description | estimate | notes |
| ----- | ----------- | -------- | ----- |
| Database availability | Unspecified | Unspecified | Unspecified |
| File storage availability | Unspecified | Unspecified | Unspecified |
| User account persistence | Unspecified | Unspecified | Unspecified |
| Account service over HTTP | Unspecified | Unspecified | Unspecified |
| Account service configuration management | Unspecified | Unspecified | Unspecified |


## Decisions Made

### Database availability

#### Scenario

**Updated from:**

- Unspecified

**To:**

- As a app service developer, I need access to the document storage solution so that I can perform necessary reads and writes to provide service to clients

#### Acceptance criteria

**Updated from:**

- Unspecified

**To:**

- [ ] MongoDB instance is running locally (preferably within a container)
- [ ] Database is accessible over a network port
- [ ] Can connect to database using [Mongosh](https://www.mongodb.com/docs/mongodb-shell/)
- [ ] Can connect to database using a [MongoDB Driver](https://www.mongodb.com/docs/drivers/)

#### Status

**Updated from:**

- Unspecified

**To:**

- Ready

### File storage availability

#### Scenario

**Updated from:**

- Unspecified

**To:**

- As a service developer, I need access to the binary large object storage solution (BLOB) so that I can perform the required read/writes to provide service to clients

#### Acceptance criteria

**Updated from:**

- Unspecified

**To:**

- [ ] MinIO service is running locally (preferably within a container)
- [ ] MinIO service is exposed through a network port
- [ ] Can connect to the service using the AWS CLI (with S3 compatibility)
- [ ] Can connect to the service using the MinIO SDK

#### Status

**Updated from:**

- Unspecified

**To:**

- Ready

### Account service configuration management

#### Scenario

**Updated from:**

- Unspecified

**To:**

- As a service developer, I want to track changes applied to the accounts service so that I can audit changes and track issues down effectively

#### Acceptance criteria

**Updated from:**

- Unspecified

**To:**

- [ ] A remote repository is set up to track the source code of the accounts service
- [ ] The remote repository can be cloned locally
- [ ] Local changes can be pushed to a remote branch
- [ ] Pushes to the main branch of the remote repository are prohibited
- [ ] Changes can be merged through approved pull requests only

#### Status

**Updated from:**

- Unspecified

**To:**

- Ready

### Account service over HTTP

#### Status

**Updated from:**

- Unspecified

**To:**

- New

### User account persistence

#### Status

**Updated from:**

- Unspecified

**To:**

- New
<!-- Agreements about readiness, phrasing, acceptance criteria, or decomposition of backlog items discussed -->
<!-- Each item discussed in the meeting should have its dedicated subsection here -->

