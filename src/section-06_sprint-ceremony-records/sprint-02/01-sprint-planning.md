# Sprint Planning - 2 (2025-09-29 - 2025-10-10)

## Sprint Goals
<!-- Clear, concise statement of sprint goal(s) -->
- Consider the data storage solutions available for the project
- Describe a process for managing the data storage solution for the project

## Capacity and Constraints
<!-- Notes about the sprint's capacity and any constraints for the upcoming sprint -->
- Only a single person (me) is working on project activities
- Expected time available will remain at 20 hours for the 2 week time-boxed period

## Selected Backlog Items

<!-- Backlog items that will be prioritized during this sprint -->

### Stories

<!-- Stories selected from the product backlog -->
<!-- These stories will be part of the sprint backlog once they've undergone task breakdown activities -->

| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Data Storage | As an application service provider, I want to persist my application data so that I may utilize structured data to effectively provide a service | Unspecified |  |
| Object Storage | As an application service provider, I want to store binary data (such as images) in a remote file system so that I can utilize them for content hydration on certain responses | Unspecified | |

### Task Breakdown

<!-- Selected stories broken down into manageable tasks to complete throughout this sprint -->
<!-- Tasks should not take more than 1 day to complete and will be the summable unit of work for estimating stories -->
<!-- Each story selected for this sprint should receive a dedicated subsection to show task breakdown and estimation -->

#### Data Storage

**Scenario**

- As an application service provider, I want to persist my application data so that I may utilize structured data to effectively provide a service

**Acceptance Criteria**

- [ ] Storage solution should allow for storing of structured data
- [ ] Storage solution should allow for querying to return a subset of stored data
- [ ] Storage solution must have interoperability with the Go programming language
- [ ] Storage solution must be tolerant of multiple read/write operations

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Examine the properties of data records in SQL-based storage solutions | Design | 0.5 hours |
| 2 | Examine the properties of data records in NoSQL-based (document) storage solutions | Design | 0.5 hours |
| 3 | Examine the properties of data records in NoSQL-based (graph) storage solutions | Design | 0.5 hours |
| 4 | Examine the properties of SQL-based query languages | Design | 0.5 hours |
| 5 | Examine the properties of NoSQL-based (document) query languages | Design | 0.5 hours |
| 6 | Examine the properties of NoSQL-based (graph) query languages | Design | 0.5 hours |
| 7 | Determine driver availability of data storage solution in Go | Back | 1 hour |
| 8 | Examine the parallelism mechanics used in SQL-based storage solutions | Design | 0.5 hours |
| 9 | Examine the parallelism mechanics used in NoSQL-based storage solutions | Design | 0.5 hours |
| 10 | Determine the most viable option for data storage with the target platform | Back | 2 hours |
| 11 | Justify the data storage choice with an architectural decision record | Design | 1 hour |

#### Object Storage

**Scenario**

- As an application service provider, I want to store binary data (such as images) in a remote file system so that I can utilize them for content hydration on certain responses

**Acceptance Criteria**

- [ ] Storage solution should offer a file system to place files
- [ ] Storage solution should be remotely accessible with the Go programming language
- [ ] Storage solution should offer CRUD operations commonly found in file systems

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Explore solutions for object storage that can hold blobs of binary data | Design | 1 hour |
| 2 | Determine how interactions occur between clients and the object storage service | Back | 2 hours
| 3 | Determine the options available to handle interactions with the object storage service through Go | Back | 3 hours |
| 4 | Explore the way the storage service handles blobs and the proper ways to manipulate them when needed | Design | 2 hours |
| 5 | Decide on an object storage service most suitable for the project and justify the choice with a architectural decision record | Design | 2 hours |

### Risks / Dependencies

<!-- List of known risks or blockers that could arise during this sprint -->
<!-- Mitigation strategies should be layed out for each risk individually -->

#### Vendor lock-in

Many data storage solutions are offered as databases-as-a-service to alleviate the hassle of administrating a database yourself. If a particular data solution is truly desirable for the project, it may only be available from these cloud-based offerings

**To mitigate:**

1) Find solutions with thriving open-source communities (for help and support)
2) Learn to avoid the databases-as-a-service trap by learning about self-hosting a database

**To control in case of risk realization:**

1) Build around the locked in component and use it as a pillar of the platform's architecture
2) Look into migrating to a different database when the opportunity arises

## Action Items

<!-- Actions to officially begin the planned sprint -->
- Find data storage solutions to consider
- Find object storage solutions to consider
