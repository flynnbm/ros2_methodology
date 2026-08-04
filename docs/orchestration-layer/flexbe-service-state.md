# FlexBE Service State

Document request construction, server availability checks, response mapping,
timeouts, and failure outcomes.

Service states should avoid blocking the behavior engine while waiting for a
response and should expose enough detail for recovery decisions.

!!! note "TODO: Planned coverage"
    Add a complete service-client state that demonstrates:

    - Request construction from userdata
    - Non-blocking server availability and response handling
    - Timeout, transport-failure, and utility-failure outcomes
    - Response mapping for later states
    - Behavior wiring and recovery transitions
    - Use with the PCL voxel-grid utility described on the
      [Services](../ros2-interfaces/services.md#a-pcl-filter-service-as-an-example)
      page
