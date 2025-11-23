# Sprint Review - 5 (2025-11-23)

## Sprint Goal Review
<!-- Review of goal(s) made during this sprint's planning meeting -->
<!-- Declare whether goals were (met / partially met / not met) and explain -->
| Goal | Status |
| ---- | ------ |
| Complete the leftover story tasks from sprint 4 | Met |
| Begin enrichment of the schema for account documents | Not met |

## Completed Work

| Story | Demoed? | Notes |
| ----- | ------- | ----- |
| User account persistence | Yes | N/A |
| Account service over HTTP | Yes | N/A |

## Incomplete Work

> All planned work was completed for this sprint

## Stakeholder Feedback
<!-- Capture of discussion about work completeness, reactions to demos, and any suggestions made -->
- Consistent JSON responses across all endpoints with make frontend handling much easier
- The context manipulation to allow requests to be processed in steps seems odd, but promising for breaking down problems

## Future Work Discussed
<!-- Initial clarifications on any suggestions made. Add to backlog, but make no commitments -->
- Testing tasks revealed testability challenges for the codebase
  - Switch to a test-driven development process
  - Take advantage of Go's powerful type system
- Intertwining of database abstraction code with service code needs to be undone
