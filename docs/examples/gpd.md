# GPD

Use this page to examine a grasp-pose-detection integration: input point clouds,
frame transformations, configuration context, invocation, output interpretation,
and failure handling.

Link the example to the relevant wrapping and ROS 2 interface guidance once those
interfaces are established.

!!! note "TODO: Planned coverage"
    Expand this case study to include:

    - GPD and `gpd_ros` requirements, relevant versions, and configuration context
    - Links to the repositories containing build and setup instructions
    - Point-cloud inputs, coordinate frames, and preprocessing requirements
    - How the underlying GPD library is exposed through ROS 2
    - Grasp-detection requests, results, and failure behavior
    - Conversion of GPD grasp poses into pipeline-friendly pose messages
    - The current two-server design and the trade-off involved in combining it
    - A representative detection workflow with visuals and expected output
    - Compatibility constraints and useful troubleshooting context
    - Links to the wrapping, service, orchestration, and MoveIt examples
