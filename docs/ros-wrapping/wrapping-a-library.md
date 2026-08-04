# Wrapping a Library

## Suggested workflow

1. Identify the smallest useful domain API.
2. Decide which calls map to topics, services, or actions.
3. Define conversions between ROS messages and domain types.
4. Keep lifecycle, threading, and error translation explicit.
5. Test the domain adapter separately from the ROS node.
6. Add launch, configuration, and integration tests.

Record constraints such as native dependencies, device access, and supported
platforms alongside the wrapper.

## GPD as a wrapping example

The [`gpd_ros` Jazzy branch](https://github.com/flynnbm/gpd_ros/tree/jazzy) is a
useful example of placing a ROS 2 boundary around software that did not originate
as a ROS component. The underlying Grasp Pose Detection (GPD) library is a C++
library built with CMake. The wrapper package builds on that library and exposes
its capabilities through ROS interfaces so they can participate in a larger ROS 2
manipulation pipeline.

The original `gpd_ros` package provided a ROS 1 wrapper. The Jazzy branch of this
fork updates that integration for ROS 2 while continuing to use the same
underlying GPD functionality. Both the original wrapper and these added utilities
are implemented in C++, matching the library they call, but clients interact with
their ROS interfaces rather than directly with the GPD API.

At a high level, the current pipeline separates two responsibilities:

1. `grasp_detection_server` accepts a point cloud, invokes GPD, and returns the
   detected `gpd::GraspPoseList` data through its service interface.
2. `grasp_pose_server` converts the detected grasp poses through the required
   matrix transformations into `geometry_msgs::PoseStamped` messages that can be
   passed to MoveIt as six-degree-of-freedom grasp poses.

This example demonstrates more than updating a ROS 1 package to ROS 2. It shows
that a separately built, non-ROS library can remain responsible for its domain
functionality while ROS 2 acts as the middleware between that functionality and
the rest of the pipeline. The wrapper owns the conversions and interface boundary;
the orchestration layer and downstream MoveIt components do not need to understand
the library's build system or internal types.

!!! note "TODO: Develop this case study"
    Expand this example with the relationship between the GPD library and wrapper
    builds, dependency declarations, CMake integration, ROS 1-to-ROS 2 changes,
    service definitions, message conversions, and the path from point-cloud input
    to a MoveIt-compatible pose. Also discuss whether the two current servers
    should remain separate or be combined behind one utility interface.

!!! note "TODO: Planned coverage"
    Expand this workflow with:

    - A small library capability carried through each wrapping step
    - Guidance for deciding what belongs inside and outside the wrapper
    - Topic, service, and action selection examples
    - Message conversion and coordinate-frame responsibilities
    - Error translation, timeouts, cancellation, and cleanup
    - Links to the examples
