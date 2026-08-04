# Orchestration Layer

The orchestration layer coordinates modular components into a larger workflow. It
decides when work should occur, manages transitions between operations, and owns
the ROS 2 clients that communicate with utility servers. It may be implemented as
a state machine, behavior tree, graphical workflow, custom script, or another tool
that can act as a compatible ROS 2 client.

The components themselves should not depend on which approach is selected. Their
service and action interfaces form the boundary that allows the orchestration
layer and the utilities to be designed, tested, and replaced independently.

## Composing utility pipelines

Designing operations as focused utility components allows the orchestration layer to
chain them into a pipeline, change their order, and expose intermediate results for
inspection. This flexibility must be weighed against the added cost of crossing
ROS 2 interfaces and converting data between operations.

!!! note "TODO: Planned coverage"
    Expand this discussion with concrete examples of:

    - Chaining focused utility servers into a pipeline
    - Reordering or substituting operations without rewriting the utilities
    - Publishing intermediate results to locate data loss or unexpected changes
    - Handling availability, timeouts, failures, cancellation, and recovery
    - Deciding when ROS 2 interface overhead is justified
    - Deciding whether tightly coupled operations should be combined instead

## FlexBE as an Example

FlexBE is the orchestration approach used by the examples in this section. It
provides concrete examples of how behavior states can interact with ROS 2 topics,
services, and actions, but it is not required by the methodology.

For each example state, this section will document inputs, outputs, outcomes,
autonomy considerations, timeouts, and cleanup behavior. The same interface and
ownership principles can be applied using another orchestration tool or custom
code.

!!! note "The central idea"
    FlexBE demonstrates one implementation of the orchestration layer. The reusable
    part of the methodology is the boundary between orchestration clients and
    modular ROS 2 utility servers, not the particular tool used on the client side.

!!! note "TODO: Section roadmap"
    Add an orchestrator-neutral workflow first, then use FlexBE to demonstrate one
    implementation. Compare the same client responsibilities in a graphical tool,
    behavior tree, state machine, and custom script without prescribing a single
    orchestrator.

!!! note "TODO: Future pipeline development"
    FlexBE won't be the only implementation we use but it is the one currently in
    use and in development. Future documentation should include other options as 
    examples to continue to draw a line between what options exist and what has been 
    used or is preferred by certain individuals or groups. Emphasize that we are not 
    intentionally promoting any one solution.
