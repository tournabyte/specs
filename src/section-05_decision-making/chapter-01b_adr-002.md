# Architectural Decision Record #2

| Field | Value |
| ----- | ----- |
| ADR Number | 002 | <!-- Numeric identifier of this ADR -->
| Title | Binary object storage solution | <!-- short, descriptive decision title -->
| Date | 2025-10-09 | <!-- Date decision made -->
| Status | Proposed | <!-- One of (Proposed/Accepted/Rejected/Superseded by/Deprecated) -->
| Last Updated | 2025-10-09 | <!-- Date of last update -->

## Context

### Background and decision necessity

As there are plans to include a web-based interface for the Tournabyte platform, it is likely that it will take advantage of popular web display components. In particular, the ability to view media files like images and video. Tournabyte aims to provide a process in which user can upload relevant content (such as a match result screenshot) and attach it to the relevant record. However, storing potentially large binary files like images is not ideal for a database management system. Thus, there is a need for a dedicated binary object service provider.

### Relevant goals, constraints, and requirements

- Follow a cloud-native application architecture
- Provide a place of user-generated files (images, video, etc.) to be stored on the server side and read by client when needed
- Avoid storing binary large objects within the selected database management system

### Referenced backlog items

- [Object Storage](https://tree.taiga.io/project/nathancmendoza-tournabyte/us/52?milestone=479657)

## Decision

### What?

The Tournabyte team has decided to utilize MinIO as the binary object storage system for the application.

### Why?

MinIO supports the S3 protocol popularized by AWS simple storage service. This protocol will make it easy to migrate (if needed) to a cloud-based storage service, most of which work on this protocol. Additionally, MinIO offers a containerized solution, making developing locally possible and cost effective.

### Who?

This decision was made by the sole member of the Tournabyte team (me)

## Options considered

<!-- One subsection per option. Consider pros, cons, costs, complexity, and risk with each -->
### Amazon S3

**Pros**

- Pioneer of the simple storage solution for binary objects
- Most popularized and available storage solution for modern application
- Free tier available for development and testing purposes

**Cons**

- Free tier limits are tight and not able to test loaded operations
- Costs associated with data operations on storage buckets

**Costs**

- Will incur costs for usage above the free tier
- Rates vary on cloud provider

**Complexity**

- Managed solution reduces complexity for binary object storage
- Key-value storage style can be easy to work with, but difficult to scale

**Risks**

- Access to free tier can be revoked at any time
- Runaway costs from usage above free tier is possible with managed solution

### MongoDB GridFS

**Pros**

- Simplifies infrastructure by using a single data storage provider for all application data needs
- Can be accessed similarly to document records and supported by most official language drivers

**Cons**

- Files are broken up into chunks and stored as partitions
- Driver reconstructs files and makes them available on demand can introduce performance concerns
- In bad taste as binary object are still being stored in database management system, even if handled differently
- No support for S3 protocol

**Costs**

- Incurred with managed MongoDB solution only

**Complexity**

- Lack of S3 protocol support would make migrating to another binary storage service difficult
- Reconstruction of binary files makes access patterns differ than an S3 supporting service

**Risks**

- Could introduce infrastructure lock-in by depending only on MongoDB

### MinIO

**Pros**

- Essentially S3, but available for local deployment
- Supports S3 protocol for easier transition, but also includes its own protocol for exclusive use
- Containerized option can simplify operational complexity

**Cons**

- MinIO protocol operates similarly to S3, but cannot be used with other storage services

**Costs**

- Costs minimal with use of containerized option

**Complexity**

- Operational complexity reduced with use of containerized option

**Risks**

- Can introduce vendor lock-in if using MinIO only protocol

## Rationale

<!-- Explain why the selected option is the best fit. Include technical and business reasoning -->
Using MinIO for the object storage service of the Tournabyte platform supports technical goals by providing a locally managed instance of the service and enabling the cloud-native approach to continue. Having a locally managed instance is nice because it avoid using any free tier resources for development and makes testing the infrastructure interactions locally much easier. Additionally, avoiding using free tier resources from a cloud provider reduces the risk of ever incurring costs from a cloud provider when using a managed storage servvice.

## Consequences

### Positives

- Testing infrastructure interactions is much easier
- More control over infrastructure setup and teardown

### Negatives

- May introduce vendor lock-in with exclusive protocol (even if similar to S3) 
- Managing instances will require additional resources beyond application development

### Operational constraints

- Containerized options should reduce operational complexity
- Using exclusive protocol may provide a better developer experience, but will make migration to cloud-based solution more difficult

## Implementation plan

### Steps to roll out

1) Configure and automate acquisition and deployment of local testing storage service
2) Application services begin using storage service for binary objects

### Timeline for work to be done

- Sprint 3: Overcome operational complexities with containerized option
- Beyond: Services use storage as part of initial designs

## Related artifacts

<!-- direct links to backlog items used in this ADR-->
<!-- related ADRs and architectural diagrams can go here -->

- [MongoDB GridFS unify infrastructure](./chapter-01a_adr-001.md)

## Changelog 

| Date | Change description | Version |
| ---- | ------------------ | ------- |
| 2025-10-09 | Initial draft | 1.0 |
