# Backlog Refinement - 2025-11-20

## Items Discussed
<!-- Items currently in the backlog that were discussed in this meeting -->
| title | description | estimate | notes |
| ----- | ----------- | -------- | ----- |
| Add account metadata fields to user account record structure | As an identity provider service, I want account documents to contain metadata fields so that the system can track account status and operational context | Unspecified | N/A |
| Database abstraction | Unspecified | Unspecified | N/A |


## Newly Identified Items
<!-- Items that were added to the backlog during this meeting -->
| title | description | estimate | notes |
| ----- | ----------- | -------- | ----- |
| Account retrieval respect metadata active flag | Unspecified | Unspecified | N/A |

## Decisions Made
<!-- Agreements about readiness, phrasing, acceptance criteria, or decomposition of backlog items discussed -->
<!-- Each item discussed in the meeting should have its dedicated subsection here -->
### Add account metadata fields to user account record structure

#### Acceptance criteria

**From:**

- [ ] The user account documents schema includes metadata fields
- [ ] The Go data structure can work with the extended schema
- [ ] The metadata fields are not user editable

**To:**

- [ ] The user account documents schema includes metadata fields
  - [] A field containing the timestamp the account was created
  - [] A field containing the timestamp the account was last modified
  - [] A field containing a flag indicating whether the account is active or not
- [ ] The Go data structure can work with the extended schema
- [ ] The metadata fields are not user editable

### Database abstraction

#### Scenario

**From:**

- Unspecified

**To:**

- As a service developer, I want a flexible wrapper around the mongoDB connection so that the service concerns itself with high level operations instead of database implementation details

#### Acceptance criteria

**From:**

- Unspecified

**To:**

- [ ] The wrapper can be configured through a connection string specifying the necessary connection details
- [ ] The wrapper can marshal go struct types with appropriate BSON tags
- [ ] The wrapper can unmarshal go struct types with appropriate BSON tags
- [ ] The wrapper provides a consistent interface for single document CRUD operations
- [ ] The wrapper provides a consistent interface for multiple document CRUD operations

#### Status

**From:**

- New

**To:**

- Ready

### Account retrieval respects metadata active flag

#### Scenario

**From:**

- Unspecified

**To:**

- As a service provider, I want to exclude inactive accounts from the search so that accounts without activity do not pollute the result set

#### Acceptance criteria

**From:**

- Unspecified

**To:**

- [ ] The ID of an account with an active metadata flag is included in a lookup query for that ID
- [ ] The ID of an account without an active metadata flag is excluded in a lookup query for that ID
- [ ] Queries for accounts whose ID is inactive are treated as missing resources

#### Status

**From:**

- New

**To:**

- Ready
