# Sprint Planning - 6 (2025-11-24 - 2025-12-06)

## Sprint Goals
<!-- Clear, concise statement of sprint goal(s) -->
- Separate service logic from database abstraction toolkit
- Begin furnishing account record documents for better metadata

## Capacity and Constraints
<!-- Notes about the sprint's capacity and any constraints for the upcoming sprint -->
- Only 1 person (me) working on the project
- About 20 hours can be dedicated to the sprint
- This sprint works around a major holiday (Thanksgiving 2025-11-27)

## Selected Backlog Items
<!-- Backlog items that will be prioritized during this sprint -->

### Stories
<!-- Stories selected from the product backlog -->
<!-- These stories will be part of the sprint backlog once they've undergone task breakdown activities -->

| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Database abstraction | As a service developer, I want a flexible wrapper around the mongoDB connection so that the service concerns itself with high level operations instead of database implementation details |  |  |
| Add account metadata fields to user account record structure | As an identity provider service, I want account documents to contain metadata fields so that the system can track account status and operational context | | |
| Account retrieval respects metadata active flag | As a service provider, I want to exclude inactive accounts from the search so that accounts without activity do not pollute the result set | | | 

### Task Breakdown
<!-- Selected stories broken down into manageable tasks to complete throughout this sprint -->
<!-- Tasks should not take more than 1 day to complete and will be the summable unit of work for estimating stories -->
<!-- Each story selected for this sprint should receive a dedicated subsection to show task breakdown and estimation -->

#### Database abstraction

**Scenario**

- As a service developer, I want a flexible wrapper around the mongoDB connection so that the service concerns itself with high level operations instead of database implementation details

**Acceptance criteria**

- [ ] The wrapper can be configured through a connection string specifying the necessary connection details
- [ ] The wrapper can marshal go struct types with appropriate BSON tags
- [ ] The wrapper can unmarshal go struct types with appropriate BSON tags
- [ ] The wrapper provides a consistent interface for single document CRUD operations
- [ ] The wrapper provides a consistent interface for multiple document CRUD operations

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Implement a configurable mongoDB connection string manager and builder | Design | 3 |
| 2 | Implement failsafes and validation for connection parts | Backend | 2 |
| 3 | Create an interface to safely build connection strings when sourcing from multiple cofiguration sources | Backend | 3 |
| 4 | Support encoding of arbitrary Go types to BSON  | Frontend | 1 |
| 5 | Support decoding of arbitrary Go types from BSON  | Frontend | 1 |
| 6 | Define interfaces for single document operations | Design | 1 |
| 7 | Define interfaces for multi-document operations | Design | 1 |

#### Add account metadata fields to user account record structure

**Scenario**

- As an identity provider service, I want account documents to contain metadata fields so that the system can track account status and operational context

**Acceptance criteria**

- [ ] The user account documents schema includes metadata fields 
  - [ ] A field containing the timestamp the account was created 
  - [ ] A field containing the timestamp the account was last modified 
  - [ ] A field containing a flag indicating whether the account is active or not
- [ ] The Go data structure can work with the extended schema
- [ ] The metadata fields are not user editable

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Update the Go type definition with the metadata fields and an appropriate types | Design | 1 |
| 2 | Migrate the database to expect and accept account records with the new fields | Backed | 2 |
| 3 | Determine the field visible when account lookup is performed | Frontend | 1 |

#### Account retrieval respects metadata active flag

**Scenario**

- As a service provider, I want to exclude inactive accounts from the search so that accounts without activity do not pollute the result set

**Acceptance criteria**

- [ ] The ID of an account with an active metadata flag is included in a lookup query for that ID
- [ ] The ID of an account without an active metadata flag is excluded in a lookup query for that ID
- [ ] Queries for accounts whose ID is inactive are treated as missing resources

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Modify the account lookup filter to include a predicate that the active flag is set | Backend | 2 |
| 2 | Enforce the unsetting of the active flag means the requested resource is missing | Frontend | 1 |


### Risks / Dependencies
<!-- List of known risks or blockers that could arise during this sprint -->
<!-- Mitigation strategies should be layed out for each risk individually -->
#### DB abstraction layer and schema misalignment

The abstraction layer may introduce expectations that may restrict the freedom currently offered by a NoSQL database

**To mitigate:**

1) Understand the BSON encoding/decoding process and how to best support it for arbitrary types
2) Attempt to allow data definitions to control the behavior of the abstraction layer

**To control in case of risk realization:**

1) Restrict the allowed types with the abstraction layer to well-known behaved types
2) Let the abstraction layer determine if a Go type is suitable for use with it

#### DB abstraction layer dependency

**To mitigate**:

1) Focus most of this sprint to implementing and testing of the DB abstraction layer

**To control in case of risk realization:**

1) Revert back to intertwined database abstraction layer with service logic
2) Identify patterns in multiple abstraction layers in use
3) Unify them into a general DB abstraction layer and replace multiple version across existing services

## Action Items
<!-- Actions to officially begin the planned sprint -->

- Begin implementation of the database abstraction layer
- Ensure testability and code coverage of the abstraction layer
