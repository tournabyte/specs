# Backlog Refinement - (2025-12-03)

## Items Discussed
<!-- Items currently in the backlog that were discussed in this meeting -->
| title | description | estimate | notes |
| ----- | ----------- | -------- | ----- |
| Blob storage abstraction | N/A | N/A | N/A |

## Newly Identified Items
<!-- Items that were added to the backlog during this meeting -->
| title | description | estimate | notes |
| ----- | ----------- | -------- | ----- |
| Account authentication | N/A | N/A | N/A |
| Database wrapper integration |  N/A | N/A | N/A |

## Decisions Made
<!-- Agreements about readiness, phrasing, acceptance criteria, or decomposition of backlog items discussed -->
<!-- Each item discussed in the meeting should have its dedicated subsection here -->

### Blob storage abstraction

#### Acceptance criteria

**From:**

- Not specified

**To:**

- [ ] The wrapper provides CRUD operations for single files
- [ ] The wrapper provides sharable links to individual files
- [ ] The wrapper handles storage solution credentials and service availability checks

#### Scenario

**From:**

- Not specified

**To:**

- As a service provider requiring access to binary object storage, I want a lightweight abstraction layer so that only the essential functionality of the storage solution is exposed

#### Status

**From:**

- New

**To:**

- Ready

### Account authentication

#### Acceptance criteria

**From:**

- Not specified

**To:**

- [ ] An API endpoint is defined for accepting and processing authorization requests
- [ ] A secure session token is provided for successful authentication 
- [ ] An error is provided for unsuccessful authentication

#### Scenario

**From:**

- Not specified

**To:**

- As a account holder, I want a RESTful API endpoint that accepts a username/password authorization scheme, validates it, and returns an access token so that other protected resources are now available

#### Status

**From:**

- New

**To:**

- Ready

### Database wrapper integration

#### Acceptance criteria

**From:**

- Not specified

**To:**

- [ ] The thin abstraction layer package becomes a dependency for service projects
- [ ] The official mongoDB go driver is removed from the list of dependencies for service projects
- [ ] Raw mongoDB driver calls are replaced with thin abstraction layer utilities

#### Scenario

**From:**

- Not specified

**To:**

- As a service provider utilizing mongoDB for record storage, I want to access such record from a thin abstraction layer instead of raw driver calls so that database access logic is consistent and flexible

#### Status

**From:**

- New

**To:**

- Ready
