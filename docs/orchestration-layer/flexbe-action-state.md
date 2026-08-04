# FlexBE Action State

Document goal creation, feedback handling, result mapping, cancellation, and
preemption. Define outcomes for rejected, aborted, canceled, and successful goals.

Include an example showing how behavior userdata maps into the goal and how the
result is returned to later states.

!!! note "TODO: Planned coverage"
    Add a complete action-client state that demonstrates:

    - Server availability and goal construction from userdata
    - Goal acceptance and rejection
    - Feedback mapping and progress reporting
    - Cancellation and preemption
    - Successful, aborted, and canceled result outcomes
    - Recovery transitions and cleanup
    - A MoveIt `move_group` request connected to the
      [Actions](../ros2-interfaces/actions.md) and [MoveIt](../examples/moveit.md)
      pages
