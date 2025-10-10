# Architectural Decision Record #001

| Field | Value |
| ----- | ----- |
| ADR Number | 001 | <!-- Numeric identifier of this ADR -->
| Title | Database management system selection | <!-- short, descriptive decision title -->
| Date | 2025-10-08 | <!-- Date decision made -->
| Status | Accepted | <!-- One of (Proposed/Accepted/Rejected/Superseded by/Deprecated) -->
| Last Updated | 2025-10-10 | <!-- Date of last update -->

## Context

### Background and decision necessity

The Tournabyte platform is intended to be a cloud-native application. Because of this path, it is necessary to store data on the server side. This will require a dedicated data storage service for the application components to use. The Tournabyte application components will access the data storage through a programmatic manner in order to provide data services to Tournabyte clients.

The decision for a database management system is required due to the circumstances of the project. The numerous options available for modern application necessitate the recording of the decision of which one to use. On top of the various styles database management system take (SQL, NoSQL, etc.), each style has multiple popular vendors that could work well with the project's direction. Deciding on the appropriate one to use will influence future architecture decisions and might impose design constraints in order to effectively use the selected system.

### Relevant goals, constraints, and requirements

- Cloud-native applications need to store application data on the server side
- Application data structure is very uncertain at the moment
- Data management requirements call for a record-keeping solution for data generated and controlled by the Tournabyte system

### Referenced backlog items

- [Data Storage](https://tree.taiga.io/project/nathancmendoza-tournabyte/us/51?milestone=479657)

## Decision

### What?

The Tournabyte team has decided on utilizing a NoSQL data solution. Additionally, the team has decided to implement data storage with the community version of [MongoDB](https://www.mongodb.com/try/download/community-edition)

### Why?

With the intent to be cloud-native, just about any popular database solution will suffice. Managed options as well as container images available for these options make it easy to start development with any of the available solutions. However, the constraint that the application data is currently uncertain makes traditional SQL solution a difficult choice. The strict schema definition would require proper migration management in order not break individual component with independent updates. Thus, the decision to use a NoSQL solution will provide the Tournabyte team with the schema flexibility necessary to quickly iterate of features of the platform. Care will still need to be taken with a more fully integrated system and changes to the system, but in early development it is ideal. The choice of MongoDB is obvious as it is the more popular NoSQL solution that is not exclusively linked to a particular cloud provider.

### Who?

The decision was made by the sole member of the Tournabyte team (me)

## Options considered

<!-- One subsection per option. Consider pros, cons, costs, complexity, and risk with each -->
### MySQL

**Pros**

- System is open-source and free to use
- Many ways to programmatically access
- Follows SQL but keeps it simple
- Not tied to a single cloud provider

**Cons**

- Strict schema does not agree with data uncertainty
- Limited built in data types may restrict structure

**Costs**

- No anticipated costs for development instances
- Managed instances will incur costs over time

**Complexity**

- Most in-line with SQL standard
- Declarative query language may introduce complex queries with normalized data
- ORM can introduce complexity and performance concerns in order to abstract data operations

**Risks**

- Database system developed independently from access
- Driver and ORM packages developed independently from database system
- Multiple access packages can be risky should maintainers abandon the project

### PostgreSQL

**Pros**

- System is open-source and free to use
- Many ways to programmatically access
- Follows SQL but includes many QoL features
- Not tied to a single cloud provider

**Cons**

- Strict schema does not agree with data uncertainty
- Limited built in data types may restrict structure

**Costs**

- No anticipated costs for development instances
- Managed instances will incur costs over time

**Complexity**

- Most in-line with SQL standard
- Declarative query language may introduce complex queries with normalized data
- ORM can introduce complexity and performance concerns in order to abstract data operations

**Risks**

- Database system developed independently from access
- Driver and ORM packages developed independently from database system
- Multiple access packages can be risky should maintainers abandon the project

### MongoDB

**Pros**

- System has a community edition that is free to use
- Definitive way to access data programmatically with official language drivers
- Flexible schema aligns well with data structure uncertainty

**Cons**

- Lack of constraint enforcement will lead to dirty duplication and query performance concerns
- Must learn to embrace the embedding of relations rather than link

**Costs**

- No anticipated costs for development instances
- Managed instances will incur costs over time

**Complexity**

- JSON query language may be difficult to navigate when querying on nested documents
- Index selection will be important for the performance of queries

**Risks**

- Database access dependent on maintaining of a community edition
- Loose scheme means documenting current document structure for code needs to be up to date wherever used

### DynamoDB

**Pros**

- Fully managed with free tier allotment
- Definitive way to access data programmatically with AWS SDK
- Flexible schema aligns well with data structure uncertainty

**Cons**

- Lack of constraint enforcement will lead to dirty duplication and query performance concerns
- Must learn to embrace the embedding of relations rather than link

**Costs**

- No anticipated costs for development instances
- Managed instances will incur costs over time
- Costs is based on operations and storage, which can balloon if not managed

**Complexity**

- JSON query language may be difficult to navigate when querying on nested documents
- Index selection will be important for the performance of queries

**Risks**

- Database access dependent on maintaining of a free tier
- Loose scheme means documenting current document structure for code needs to be up to date wherever used

### Neo4j

This options was briefly considered, but not explored due to a mismatch in use case

## Rationale

<!-- Explain why the selected option is the best fit. Include technical and business reasoning -->
MongoDB is the best fit option for the Tournabyte team because of the flexibility it provides. The schema flexibility fits nicely into the structure uncertainty at this stage of the project. The schemaless operation will allow application component to free explore the appropriate data structuring they need. This means that application code will dictate the structure of the data and will be the source of truth for the document structure the component expect. Failure at the application component level would indicate bad/corrupt data, since the schema is defined outside the database.

Additionally, the hosting options can help with business concerns. At this moment, funding is limited, so the community edition is a savior. While it may add complexity to the overall infrastructure, this free option will be the best options for the project's wallet. A managed solution may be considered with a more completed product, but the business costs and not be endured without generating any revenue

## Consequences

### Positives

- Popular option selected supported by most popular cloud providers to maintain cloud-native posture
- Free community addition will not incur development costs

### Negatives

- Administration complexities added to project requirements by selecting community edition
- Schema tracking no longer systematic and is based on whether components can work with current document structures

### Operational constraints

- None identified

## Implementation plan

### Steps to roll out

1) Include database administration tasks in the upcoming sprints
2) Modify user account service to utilize a database instance instead of a file
3) Future service should be built to work with a database 

### Timeline for work to be done

- Sprint 3: database administration and automation tasks
- Sprint 4: migrate user account service to database capabilities 
- Beyond: services use database as official data store

## Related artifacts

<!-- direct links to backlog items used in this ADR-->
<!-- related ADRs and architectural diagrams can go here -->
N/A

## Changelog 

| Date | Change description | Version |
| ---- | ------------------ | ------- |
| 2025-10-08 | Initial draft | 1.0 |
| 2025-10-10 | Status update | 1.0 |
