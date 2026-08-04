# Package Layout

A wrapper often benefits from keeping node setup, conversions, and domain adapters
in separate modules.

!!! note "A known-working package pattern"
    This page may look more like a direct how-to guide than other parts of this
    methodology, but the layout is not intended as the only valid ROS 2 package
    structure. It documents a repeatable format for creating ROS 2 utility
    packages that is already known to work in a modular pipeline.

    The [`pcl_ros2` package](https://github.com/uml-robotics/pcl_ros2/tree/main)
    provides a concrete example of this approach. Following a comparable structure
    gives a project a consistent, reviewable starting point and helps demonstrate
    that its organization follows a tested methodology. The example will be
    examined in more detail as this section develops.

```text
my_wrapper/
├── config/
├── launch/
├── my_wrapper/
│   ├── adapters/
│   ├── conversions.py
│   └── node.py
├── resource/
├── test/
├── package.xml
└── setup.py
```

Adapt this structure for `ament_cmake` packages and compiled libraries as needed.

!!! note "TODO: Planned coverage"
    Add parallel Python and C++ layouts and explain:

    - Where nodes, library adapters, and message conversions belong
    - How interface definitions are separated from their implementations
    - Where launch files, parameters, and configuration files belong
    - How dependencies are declared in `package.xml` and the build system
    - Where unit, integration, and launch tests fit
    - Which parts are conventions and which are required by ROS 2
