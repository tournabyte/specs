# Sprint Planning - 3 (2025-10-13 - 2025-10-24)

## Sprint Goals
<!-- Clear, concise statement of sprint goal(s) -->
- Gain access to the data management tools selected during the previous sprint with appropriate tooling
- Begin tracking development of the Tournabyte backend services

## Capacity and Constraints
<!-- Notes about the sprint's capacity and any constraints for the upcoming sprint -->
- Only 1 team member(me) currently working on the project
- Capacity has settled to about 25 story points per sprint, depending on story complexity

## Selected Backlog Items
<!-- Backlog items that will be prioritized during this sprint -->

### Stories
<!-- Stories selected from the product backlog -->
<!-- These stories will be part of the sprint backlog once they've undergone task breakdown activities -->

| Title | Description | Estimate | Notes |
| ----- | ----------- | -------- | ----- |
| Account service configuration management | As a service developer, I want to track changes applied to the accounts service so that I can audit changes and track issues down effectively | 4 | Configuration managemnt |
| Database availability | As a app service developer, I need access to the document storage solution so that I can perform necessary reads and writes to provide service to clients | 7 | Data management |
| File store availability | As a service developer, I need access to the binary large object storage solution (BLOB) so that I can perform the required read/writes to provide service to clients | 10 | Data management |

### Task Breakdown
<!-- Selected stories broken down into manageable tasks to complete throughout this sprint -->
<!-- Tasks should not take more than 1 day to complete and will be the summable unit of work for estimating stories -->
<!-- Each story selected for this sprint should receive a dedicated subsection to show task breakdown and estimation -->

#### Account service configuration management

**Scenario**

As a service developer, I want to track changes applied to the accounts service so that I can audit changes and track issues down effectively

**Acceptance criteria**

- [ ] A remote repository is set up to track the source code of the accounts service
- [ ] The remote repository can be cloned locally
- [ ] Local changes can be pushed to a remote branch
- [ ] Pushes to the main branch of the remote repository are prohibited
- [ ] Changes can be merged through approved pull requests only

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Initialize the remote git repository on GitHub for the account service | Backend | 0.5 |
| 2 | Set up a local repository to track the account service repository | Frontend | 0.5 |
| 3 | Initialize a go module in the repository for the account service | Frontend | 0.5 |
| 4 | Write a simple README file for the account service | UX | 1 |
| 5 | Create a root commit in the local repository containing the initialized go module and the README file | Frontend | 0.5 |
| 6 | Push the initial commit to the remote repository | Frontend | 0.5 |
| 7 | Setup branch protection on the remote repository to prevent pushes directly to main branch | Backend | 0.5 |

#### Database availability 

**Scenario**

As a app service developer, I need access to the document storage solution so that I can perform necessary reads and writes to provide service to clients

**Acceptance criteria**

- [ ] MongoDB instance is running locally (preferably within a container)
- [ ] Database is accessible over a network port
- [ ] Can connect to database using [Mongosh](https://www.mongodb.com/docs/mongodb-shell/)
- [ ] Can connect to database using a [MongoDB Driver](https://www.mongodb.com/docs/drivers/)

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Configure a local instance of MongoDB | Backend | 2 |
| 2 | Expose the local instance over a network input | Backend | 1 |
| 3 | Install the MongoSH tool to create interactive sessions with the local instance | Frontend | 0.5 |
| 4 | Demonstrate that interactive sessions with the local instance work | UX | 1 |
| 5 | Install the MongoDB go driver to access the local instance programmatically | Frontend | 0.5 |
| 6 | Demonstrate that programmatic sessions work with the local instance | UX | 2 |

#### File store availability 

**Scenario**

As a service developer, I need access to the binary large object storage solution (BLOB) so that I can perform the required read/writes to provide service to clients

**Acceptance criteria**

- [ ] MinIO service is running locally (preferably within a container)
- [ ] MinIO service is exposed through a network port
- [ ] Can connect to the service using the AWS CLI (with S3 compatibility)
- [ ] Can connect to the service using the MinIO SDK

**Tasks**

| Task Number | Task Description | Task Type | Task Estimate |
| ----------- | ---------------- | --------- | ------------- |
| 1 | Configure a local MinIO instance | Backend | 2 |
| 2 | Expose the local instance through a network port | Backend | 1 |
| 3 | Download and install the AWS CLI for interactive sessions | Frontend | 1 |
| 4 | Configure the AWS CLI to create interactive sessions with the local instance instead of AWS | UX | 2 |
| 5 | Demonstrate the interactive sessions work with the local instance | UX | 2 |
| 6 | Download and install the MinIO SDK for programmatic sessions | Frontend | 1 |
| 7 | Demonstrate the programmatic sessions work with the local instance | UX | 1 |

### Risks / Dependencies
<!-- List of known risks or blockers that could arise during this sprint -->
<!-- Mitigation strategies should be laid out for each risk individually -->
#### Vendor lock-in

The decision to use the MinIO SDK for the blob storage service will provide a better developer experience, but will not allow use with other similar storage solution

**To mitigate:**

1) Write clean and maintainable code to interact with the blob storage service
2) Understand the similarities between MinIO interactions and how they could map to a more widely supported protocol like S3

**To control in case of risk realization:**

1) Switch dependencies to use S3 protocol instead
2) Utilize clean and maintainable code to ease protocol transition for the blob storage service

## Action Items
<!-- Actions to officially begin the planned sprint -->
- Look into container customization with MongoDB and MinIO images
- Consider how to track configuration and automate setup and teardown of the images
