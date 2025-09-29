# Sprint Planning - 1 (2025-09-15 - 2025-09-26)

## Sprint Goals
<!-- Clear, concise statement of sprint goal(s) -->

- Establish the capability to document design decisions and track changes made to work products

## Capacity and Constraints

<!-- Notes about the sprint's capacity and any constraints for the upcoming sprint -->
- Only one team member (me) performing project activities
- Coursework increasing could limit time for project to ~20 hours for the sprint

## Selected Backlog Items

<!-- Backlog items that will be prioritized during this sprint -->

### Stories

<!-- Stories selected from the product backlog -->
<!-- These stories will be part of the sprint backlog once they've undergone task breakdown activities -->

| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Configuration Management | As a developer, I want to apply version control to the projects source code so that I can track project progress and manage issues in a structured manner. | 3 hours | Story is a team requirement |
| User Accounts | As a platform user, I want to have an identity to distinguish myself from other platform users. | 15 hours | |

### Task Breakdown

<!-- Selected stories broken down into manageable tasks to complete throughout this sprint -->
<!-- Tasks should not take more than 1 day to complete and will be the summable unit of work for estimating stories -->
<!-- Each story selected for this sprint should receive a dedicated subsection to show task breakdown and estimation -->

#### Configuration Management

**Scenario**

As a developer, I want to apply version control to the projects source code so that I can track project progress and manage issues in a structured manner.

**Acceptance Criteria**

- [ ] Determine the version control system that will be used
- [ ] Setup the remote side of the project
- [ ] Ensure the appropriate version control tool can utilize the remote side of the project

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Find version control systems available for configuration management of the project | Back | 0.5 hour |
| 2 | Evaluate associated costs with using discovered version control systems | Back | 1 hour |
| 3 | Establish identity (create account if needed) with selected version control system | Back | 0.5 hour |
| 4 | Create the repositories for which code and other work products are to be tracked and stored | Back | 0.5 hour |
| 5 | Create root commits for the project repositories | Back | 0.5 hour |

#### User Accounts

**Scenario**

As a platform user, I want to have an identity to distinguish myself from other platform users.

**Acceptance Criteria**

- [ ] The system uniquely identifies accounts from each other
- [ ] The unique identifier is automatically assigned to new accounts
- [ ] The unique identifier is not mutable by platform clients
- [ ] The unique identifier does not impose itself on any resources created or maintained by the user account

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Decide on an identifier to use for user accounts | Design | 2 hours |
| 2 | Find a go module that supports use of the selected unique identifier | Design | 2 hours |
| 3 | Decide on additional fields that represent a user account on the platform | Design | 1 hour |
| 4 | Implement an account creation service | Back | 5 hours |
| 5 | Implement an account lookup service | Back | 5 hours |

### Risks / Dependencies

<!-- List of known risks or blockers that could arise during this sprint -->
<!-- Mitigation strategies should be layed out for each risk individually -->
#### Limits on free tiered cloud version control

Many cloud-based SaaS will offer their services to customer for free with the caveat the their resource utilization does not exceed a threshold. Additionally, some features may be restricted to paying customers and may not be available with the free tier. 

**To mitigate:**

1) Determine which version control system is most generous and join them
2) Stick with plain text formats wherever possible to minimize file storage used

**To control in case of risk realization:**

1) Trim artifacts that can be reproduced or built on demand from source trees
2) Consider a paid plan if usage still exceeds free-tier limits

## Action Items

<!-- Actions to officially begin the planned sprint -->
- Prepare and utilize a decision-making process that can be recorded for the "User Accounts" story
