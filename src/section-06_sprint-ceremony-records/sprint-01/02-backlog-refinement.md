# Backlog Refinement - (2025-09-25)

## Items Discussed
<!-- Items currently in the backlog that were discussed in this meeting -->

| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Permissions and security | As a platform user, I want to have secure access to my platform data and have appropriate CRUD permissions based on my associations so that I can effectively use the platform to both participate and manage platform events. | 30 hours |  |

## Newly Identified Items
<!-- Items that were added to the backlog during this meeting -->

| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Data Storage | Unspecified | Unspecified | |
| Object Storage | Unspecified | Unspecified | |

## Decisions Made

<!-- Agreements about readiness, phrasing, acceptance criteria, or decomposition of backlog items discussed -->
<!-- Each item discussed in the meeting should have its dedicated subsection here -->

### Permissions and Security

#### Status

**Updated from:**

- Ready

**To:**

- Needs Info

### Data Storage

#### Scenario

**Updated from:**

- Unspecified

**To:**

- As an application service provider, I want to persist my application data so that I may utilize structured data to effectively provide a service

#### Acceptance Criteria

**Updated from:**

- Unspecified

**To:**

- [ ] Storage solution should allow for storing of structured data
- [ ] Storage solution should allow for querying to return a subset of stored data
- [ ] Storage solution must have interoperability with the Go programming language
- [ ] Storage solution must be tolerant of multiple read/write operations

#### Status

**Updated from:**

- New

**To:**

- Ready

### Object Storage

#### Scenario

**Updated from:**

- Unspecified

**To:**

- As an application service provider, I want to store binary data (such as images) in a remote file system so that I can utilize them for content hydration on certain responses

#### Acceptance Criteria

**Updated from:**

- Unspecified

**To:**

- [ ] Storage solution should offer a file system to place files
- [ ] Storage solution should be remotely accessible with the Go programming language
- [ ] Storage solution should offer CRUD operations commonly found in file systems

#### Status

**Updated from:**

- New

**To:**

- Ready
