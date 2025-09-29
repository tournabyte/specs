# Sprint Planning - 00 (2025-09-02 - 2025-09-12)

## Sprint Goals

<!-- Clear, concise statement of sprint goal(s) -->
- Learn the basics of Golang and become comfortable enough to independently write Go code
- Explore the Golang ecosystem and discover how Go code is packaged and reused

## Capacity and Constraints

<!-- Notes about the sprint's capacity and any constraints for the upcoming sprint -->
- Only a single team member (me) actively working on project activities
- Project activities are not the priority with concurrent coursework taking place as well

## Selected Backlog Items

<!-- Backlog items that will be prioritized during this sprint -->

### Stories

<!-- Stories selected from the product backlog -->
<!-- These stories will be part of the sprint backlog once they've undergone task breakdown activities -->

| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Basics of Golang | As a developer, I want to learn the ropes of golang so that I am prepared write production code using this language. | 20 hours | Story is a team requirement |
| Golang ecosystem | As a developer, I want to explore the golang module ecosystem so that I can leverage existing projects and integrate my own modules seamlessly. | 20 hours | Story is a team requirement |
| Configuration Management | As a developer, I want to apply version control to the projects source code so that I can track project progress and manage issues in a structured manner. | 3 hours | Story is a team requirement |

### Task Breakdown

<!-- Selected stories broken down into manageable tasks to complete throughout this sprint -->
<!-- Tasks should not take more than 1 day to complete and will be the summable unit of work for estimating stories -->
<!-- Each story selected for this sprint should receive a dedicated subsection to show task breakdown and estimation -->

#### Basics of Golang

**Scenario**

As a developer, I want to learn the ropes of golang so that I am prepared write production code using this language.

**Acceptance Criteria**

- [ ] Understand the basic syntax rules of Golang
- [ ] Understand the programming paradigms available with Golang
- [ ] Learn about the existence of utility modules that are useful within full stack development (stdlib or third-party)
- [ ] Learn about structuring a project appropriately for full stack development

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Download and install the latest stable version of Golang | Back | 1 hour |
| 2 | Learn how to use essential Go command line tools | Back | 2 hours |
| 3 | Configure editor to work with Go source code (syntax highlighting, error detection) | Back | 1 hour |
| 4 | Core syntax of Go | Back | 2 hours |
| 5 | Data types in Go | Back | 2 hours |
| 6 | Error handling in Go | Back | 1 hour |
| 7 | Interfaces and composition in Go | Back | 1 hour |
| 8 | Concurrency in Go | Back | 3 hours |
| 9 | Memory and performance considerations | Back | 1 hour |
| 10 | Practical exercises in Go | Back | 6 hours |

#### Golang ecosystem

**Scenario**

As a developer, I want to explore the golang module ecosystem so that I can leverage existing projects and integrate my own modules seamlessly.

**Acceptance Criteria**

- [ ] Know where to find information on existing modules (docs, repos)
- [ ] Know how to install existing modules to a new project
- [ ] Learn how to manage modules that a project depends on
- [ ] Learn how to package source files into a modules that can be installed in another project

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Learn about the core standard library | Back | 3 hours |
| 2 | Learn about writing tests in Go | Back | 5 hours |
| 3 | Explore Go's dependency management system | Back | 3 hours |
| 4 | Get comfortable with creating and structuring Go modules | Back | 8 hours |
| 5 | Explore third-party modules to subsidize lean stdlib | Back | 1 hour |

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

### Risks / Dependencies

<!-- List of known risks or blockers that could arise during this sprint -->
<!-- Mitigation strategies should be layed out for each risk individually -->

#### Language volatility

The Go programming language is a fairly new language in the programming space. While not in a pre-release stage, it has established a stable release pattern. The language is rather feature-sparse compared to established industry standards. This makes it really easy and quick to pick up, but the lack of features could limit or constrain development of the project. Plans to mitigate these issues are as follows

**To mitigate:**

1) Stick with the stable version of the Go language standard and the Go tools
2) Monitor Go project status for any outlandish improvements that will likely be merged into the stable branch

**To control in case of risk realization:**

1) Stick to a particular version of Go if the project goes awry
2) Ensure all packages under this projects umbrella compile with and use the decided Go version tool set
3) Do not adopt a newer version of Go unless absolutely necessary (security issue, etc.)

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
1) Find resources on Go that can assist with learning the language
