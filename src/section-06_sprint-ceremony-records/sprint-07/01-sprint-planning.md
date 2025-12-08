# Sprint Planning - 7 (2025-12-08 - 2025-12-21)

## Sprint Goals
<!-- Clear, concise statement of sprint goal(s) -->
- Enable account security measures with password authentication
- Implement a password authentication workflow for authorization

## Capacity and Constraints
<!-- Notes about the sprint's capacity and any constraints for the upcoming sprint -->
- Only 1 person (me) working on the project
- About 20 hours can be dedicated to the sprint
- This sprint runs through semester finals week (week of 2025-12-15)

## Selected Backlog Items
<!-- Backlog items that will be prioritized during this sprint -->

### Stories
<!-- Stories selected from the product backlog -->
<!-- These stories will be part of the sprint backlog once they've undergone task breakdown activities -->
| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Add authentication fields to user account records | As an identity provider service developer, I want each user account record to include password authentication fields so that the system can securely manage password-based authentication | TODO | N/A |
| Account authentication | As a account holder, I want a RESTful API endpoint that accepts a username/password authorization scheme, validates it, and returns an access token so that other protected resources are now available | TODO | N/A |

### Task Breakdown
<!-- Selected stories broken down into manageable tasks to complete throughout this sprint -->
<!-- Tasks should not take more than 1 day to complete and will be the summable unit of work for estimating stories -->
<!-- Each story selected for this sprint should receive a dedicated subsection to show task breakdown and estimation -->
#### Add authentication fields to user account records

**Scenario**

- As an identity provider service developer, I want each user account record to include password authentication fields so that the system can securely manage password-based authentication

**Acceptance criteria**

- [ ] User account documents enable password-based authentication
- [ ] User account logins have a limited number of retries before disabling
- [ ] Service can work with updated document structure
- [ ] Sensitive fields are not exposed in API responses

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Account document structure contains a password field for authenticating | Design | 2 |
| 2 | Account doucment structure contains a field to track unsuccessful login attempts | Design | 1 |
| 3 | Successful logins reset the login attempt counter | Backend | 1 |
| 4 | Authorization checks are not performed if login attempt to too high | Backend | 2 |
| 5 | Account creation requires an initial password for the new password field | Frontend | 1 |
| 6 | Account retrieval projects the current account document to hide password info | Frontend | 1 |
| 7 | Login attempts utilize the email field as the login ID for login attempts | Backend | 2 |

#### Account authentication

**Scenario**

- As a account holder, I want a RESTful API endpoint that accepts a username/password authorization scheme, validates it, and returns an access token so that other protected resources are now available

**Acceptance criteria**

- [ ] An API endpoint is defined for accepting and processing authorization requests
- [ ] A secure session token is provided for successful authentication 
- [ ] An error is provided for unsuccessful authentication

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | The endpoint accepts the login ID + password combination as a JSON body in the request | Frontend | 2 |
| 2 | Handler function extracts required elements from body and compares them to stored credentials | Backend | 1 |
| 3 | Handler function generates an access token for authorization when comparison succeeds | Backend | 2 |
| 4 | Handler function generates an access denied message when comparison fails | Backend | 2 |
| 5 | The endpoint responds to requests using a JSON body in the response | Frontend | 1 |

### Risks / Dependencies
<!-- List of known risks or blockers that could arise during this sprint -->
<!-- Mitigation strategies should be layed out for each risk individually -->
#### Secrets storage

The storing of passwords in a database is sensitive information that must not be exposed 

**To mitigate:**

1) Avoid storing passwords in plaintext, using a hashing and salting approach instead
2) Add projections to find operations to hide stored password fields

**To control in case of risk realization:**

1) Implement other authentication methods such as OAuth or passkeys
2) Disable traditional password authentication

## Action Items
<!-- Actions to officially begin the planned sprint -->

- Find out best practices with hashing/salting in go
- See if a third-party package deals with this already
- Determine the structural changes that will occur with the additional password field
