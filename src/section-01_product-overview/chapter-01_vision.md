# Chapter 1: Product Vision

This page outlines the vision for Tournabyte, which aims to provide a cloud-native and complete suite of competitive organizations tools for e-sports organizations. The current solutions for e-sports organizations are held behind paywalls or are a fragmented collection of tools that can make processes cumbersome. This can make it particularly difficult for grass root organizations to gain momentum as economic or technical resources can be a limiting constraint.

## Context

In 1972, a group of students gathered at Stanford University, not to attend a lecture but to participate in the world’s first formally recognized video game tournament. This tournament, known as the Intergalactic Spacewar! Olympics awarded the victor with a year’s subscription to Rolling Stone magazine. While this event didn't involve flashy computer systems or live streaming, it was a revolutionary step in organized competitive gaming. Players competed for the highest score in a single-player game instead of facing off in a multiplayer arena associated with the e-sports scene.  Organizers demonstrated that it is possible to coordinate multiple matches and determine a winner amongst a pool of participants. However, it also hints at the underlying complexities that could emerge with increasing player counts and geographic range. It highlights the necessity for robust infrastructure, clear rule sets, and logistical foresight as future tournaments expand far beyond the modest scope of a single university gathering.

At the scale of a small university gathering, core organizational tasks, such as player registration, match scheduling, and determining elimination rules, can often be handled manually or with ad-hoc solutions like paper brackets or spreadsheets. Informal coordination and on-the-fly adjustments may suffice when dealing with a dozen participants in a single location. However, as tournaments scale to accommodate cross-regional participation, hundreds or even thousands of players, and simultaneous matches across multiple time zones, these amateur methods quickly become unmanageable. Delays, mismatched pairings, rule disputes, and data inconsistencies can derail the competitive experience and erode participant trust. To maintain fairness, consistency, and operational efficiency at scale, there is a clear need for a purpose-built platform. Tournabyte aims to be that platform to centralize registration, automate scheduling, enforce rule sets, and offer real-time oversight of tournament progression.

## Goals and Objectives

The primary objective of this project is to develop a unified platform tailored for e-sports organizations. It should equip them with a comprehensive toolset necessary for effective management and streamlined operation. Before diving into development, surveying the existing solutions is critical for success. This analysis should include open-source and commercial products. It will assist with assessing current capabilities, identifying gaps, and determining the feasibility of creating a more integrated and tailored solution.

### Problem Statement

As of writing, very few comprehensive resources are known for new or existing e-sports organizations to adopt. That is to say, there is currently no well-known comprehensive solution to assist with managing and operating an e-sports organization. Digging deeper for potential solutions reveals price tags that may not be attainable for grassroots communities or technical barriers discouraging adoption. In place of these solutions, organizations tend to gravitate towards various single-purpose tools and home-grown processes that fail to scale and hinder operational effectiveness.

This tool fragmentation creates significant operational inefficiencies. When organization staff rely on multiple disconnected tools, it creates silos of information that are difficult to reconcile. The lack of integration can result in duplicate efforts, inconsistent data, and increased administrative overhead as staff must manually transfer data from one tool to another. With the hindrance to collaboration and decision-making that fragmented tooling creates, it can impact an e-sports organization’s ability to respond quickly to opportunities and issues.

Tool fragmentation also places an administrative burden on organization staff, which may consist of volunteers. Experience has shown that this burden stays internalized with the staff members. However, if poor planning and decision-making occur, this can easily bleed over to the participant side and deter players from taking part in an emerging organization. The constant need for manual intervention for trivial issues prevents the organization from allocating resources to branding, growth, and other important matters pertaining to the organization’s outreach goals. It can increase staff turnover as they burn out from organizational red tape. Such challenges threaten the organization's long-term sustainability and undermine its ability to build a reputable and engaging presence within gaming communities.

### Project Goals

With the objective to build a unified e-sports management solution in mind, establishing a well-defined scope is critical for success. The current landscape of the solution space makes it too easy to simply cram together all the single-purpose solutions used to address individual problems. Doing this will almost certainly guarantee project failure due to uncontrolled scope creep. To prevent this scenario from occurring, a proper exploration phase must occur before writing any code. This phase will allow discovering pain points with fragmented tooling and existing solutions. The discovered information will assist with determining an appropriate feature set that is feasible to implement within the project timeline and will prevent uncontrolled scope creep. By taking this approach, the project can remain manageable and strategically aligned with the core needs of e-sports organizations, significantly increasing its chances of successful delivery.

In addition to the discussed platform, it should exhibit specific attributes that would make adopting the platform easy for newly founded esports organizations. In particular, there should be sufficient documentation to set up the virtual organization and enough guidance to begin management activities. This task is achievable by ensuring the resulting product addresses discovered pain points appropriately. From a more technical standpoint, the platform must be decomposable into elements supporting the entire application. This requirement for implementation suggests that a cloud-native approach for the platform is most helpful for achieving the goal. Pairing this approach with an agile process will help alleviate the uncertainty surrounding the system’s requirements. By combining thoughtful design, accessible onboarding, and adaptable development practices will help present the platform as a practical, scalable solution that lowers barriers to entry and supports the long-term growth of emerging e-sports organizations.

Lastly, providing a working instance of the platform will showcase the capabilities of the completed product. The example instance can act as a ready-to-use demonstration of the system. Having this on hand can be a helpful tool in convincing potential organizations to migrate or adopt the system. It serves as a practical proof of concept and a valuable resource for onboarding and building confidence among prospective users.

## Key Features and Capabilities

- Create and customize a player's profile
- Create and customize a team's roster and profile
- Create and customize a tournament or event as part of a organization
- Create and customize a organization to host events
- Setup event to allow for registrations of players or teams
- Generate a tournament bracket to measure progress of an event
- Schedule a match of a tournament to take place
- Report the results of a match to progress further in a tournament bracket

## Design Principles

- Follow a cloud-native design
  - Application services are to be containerized so that they can be hosted with minimal overhead
  - Application hosting can be done through native cloud services that offer basic VM rentals for container execution
  - Application hosting can be done through self-hosted hardware with proper container support
- Follow a micro-services architecture
  - Services a divided to handle singular aspects of the application service layer
  - Services will communicate each other to access each other data when needed
  - Services will own the data they control

## Technical Requirements

| Resource | Required for | Acquired from |
| -------- | ------------ | ------------- |
| Development tools (text editors, compilers, etc.) | Developing application modules | Appropriate language tooling; no anticipated cost |
| Container runtime | Complying with anticipated cloud-native design | Docker or similar technologies, no anticipated cost |
| Configuration Management | Tracking development progress | Git or similar version control tool, no anticipated cost |
| Project planning tool | Planning sprints and tracking sprint execution | Taiga due to prior experience, no anticipated cost |
| Datastore | Storing application data | Docker image for an appropriate DBMS |

## Timeline

Anticipating continuous development through May 2026 under an agile methodology

## Metrics for Success

- Delivery of source code
- Proper documentation of product
- Demonstration of properly executing software
