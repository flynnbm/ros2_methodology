# ROS Wrapping

Wrapping exposes a non-ROS library through stable ROS interfaces while preserving
a clean boundary between domain behavior and ROS transport.

The pages in this section cover the wrapping workflow, package organization, and
interface design.

!!! note "TODO: Planned coverage"
    Develop this section around the same progression used by the ROS 2 interface
    pages:

    - Explain when a library benefits from a ROS 2 wrapper
    - Define the boundary between library logic, conversions, and ROS transport
    - Show how to select and design the wrapper's ROS 2 interface
    - Compare Python and C++ package and node structures
    - Cover configuration, launch files, errors, testing, and documentation
    - Connect each design choice to a complete pipeline example

!!! note "The central idea"
    A wrapper should expose a useful capability through a stable ROS 2 contract
    without forcing clients to depend on the underlying library's implementation.
