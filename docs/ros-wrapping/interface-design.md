# Interface Design

ROS 2 interfaces form the contract between an orchestration-layer client and a
utility server. A well-designed interface describes the capability the client can
request without exposing unnecessary details from the library that performs the
work.

This page will focus on how to shape that contract, particularly through custom
`.srv` and `.action` files. It is intended as a style and methodology guide rather
than a step-by-step tutorial for writing client or server code.

## Design goals

- Select a service or action based on the interaction the client needs, not on the
  structure of the underlying library API.
- Define requests and goals that contain everything the utility needs to begin a
  well-scoped operation.
- Return responses and results that let the orchestration layer make its next
  decision without knowing the utility's internal implementation.
- Use action feedback for meaningful progress or state information rather than
  exposing low-level processing details.
- Reuse established ROS 2 message types when their meaning fits, and define custom
  messages when they make the contract clearer or more consistent.
- Represent success, partial results, and failures in a form that clients can act
  on predictably.
- Keep the contract independent of FlexBE or any other particular orchestration
  implementation.

## Review checklist

- Does the interface describe one clear utility capability?
- Is a service or action the simplest interface that provides the required client
  control?
- Do the request or goal fields provide the complete input to the operation?
- Do the response or result fields provide enough information for the client's
  next decision?
- If it is an action, is each feedback update useful to the client while the work
  is running?
- Can standard message types express the data without losing its meaning?
- Are names, units, coordinate frames, and timestamps unambiguous?
- Can invalid or partial results be represented?
- Is the interface extensible without changing established meaning?
- Are status and error values actionable by clients?
- Does the definition avoid leaking library-specific types or orchestration-layer
  assumptions across the boundary?

!!! note "TODO: Planned coverage"
    Develop this page around the design of useful ROS 2 contracts:

    - Compare when to define a `.srv` file and when to define an `.action` file
    - Explain how to divide information among service requests and responses
    - Explain how to divide information among action goals, feedback, and results
    - Show how to select, combine, or define message types for each part
    - Cover names, units, coordinate frames, timestamps, defaults, and optional data
    - Establish consistent patterns for status, errors, and partial results
    - Discuss interface evolution without tying definitions to library internals
    - Review effective and ineffective contracts from the pipeline examples

    The examples should illustrate design choices without becoming tutorials on
    the mechanics of implementing client and server nodes. Interface selection
    remains grounded in the [ROS 2 Interfaces](../ros2-interfaces/index.md)
    guidance.

!!! note "The central idea"
    The `.srv` or `.action` definition is the shared boundary: it should give the
    orchestration layer the control and information it needs while allowing the
    utility and its underlying library to remain independently replaceable.
