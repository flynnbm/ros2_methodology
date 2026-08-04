# FlexBE Subscriber State

Document topic and QoS configuration, message filtering, timeout behavior, and how
received fields map to userdata and outcomes.

Call out whether old messages are acceptable when entering the state and how the
state distinguishes missing data from invalid data.

!!! note "TODO: Planned coverage"
    Add a minimal subscriber state with its topic configuration, message filtering,
    timeout behavior, userdata mapping, and outcomes. Show how the state fits into
    a behavior and how received data is validated before the next operation runs.

    Explain that the topic is the reusable boundary in this case, while the
    subscriber implementation is more closely integrated with FlexBE. Link back to
    the general [Subscribers](../ros2-interfaces/subscribers.md) guidance.
