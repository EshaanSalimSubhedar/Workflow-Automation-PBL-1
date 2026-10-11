# BPMN 2.0 Modeling Checklist

## Before submission
- [ ] One clear start event and meaningful end events for all terminal outcomes.
- [ ] Happy path can be traced without guessing.
- [ ] Pools/lanes identify who performs each activity.
- [ ] Task type matches the work (human, automated, rule-driven, send/receive).
- [ ] Gateway type matches the logic (exclusive = one path; parallel = all paths; inclusive = one or more; event-based = first event wins).
- [ ] Gateway outgoing conditions are labeled.
- [ ] Parallel split has a logically correct join.
- [ ] Intermediate events are attached to the correct point in the flow.
- [ ] Boundary events are visibly attached to their activity/sub-process.
- [ ] Error events are not used as generic business-decision branches.
- [ ] Timer deadlines and retry counts are explicit.
- [ ] Alternate paths cover validation, external dependency, timeout, rejection, cancellation, and system failure where relevant.
- [ ] Compensation is used only when prior completed work needs to be offset.
- [ ] Every loop has an exit and maximum attempts.
- [ ] Diagram is readable at presentation size and avoids crossing lines where possible.
- [ ] Failure-path register IDs can be traced to diagram labels or annotations.
