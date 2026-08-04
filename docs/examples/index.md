# Examples

The examples are informative case studies of components and integrations used to
develop this methodology. They explain what each system does, how its components
interact, where it fits in a pipeline, and why particular design choices were
made. They are not intended to be start-to-finish replication tutorials.

Each page may include architecture diagrams, output visuals, relevant versions,
requirements, dependencies, configuration context, and links to the packages that
were used. Readers who want to run an example can follow those repositories and
their setup instructions, but reproducing the complete environment is outside the
scope of this methodology guide.

This distinction is important because a complete manipulation example may depend
on a particular Ubuntu and ROS 2 environment, source-built software, package
changes, multiple workspaces, robot or simulation configuration, and substantial
processing resources. Compatibility will vary, and the ability to reproduce that
environment is not required to understand the architectural lesson demonstrated
by the example.

The examples should therefore **show and explain** rather than ask the reader to
follow along. They can describe the relevant setup so that the system and its
constraints are understandable, while detailed installation and execution
instructions remain with the linked repositories.

!!! note "TODO: Example format"
    Develop each example using a consistent structure:

    - Purpose and relationship to the methodology
    - A high-level view of the system and the role of each component
    - ROS 2 interfaces and component ownership
    - Relevant requirements, dependencies, versions, and configuration context
    - Links to source repositories and their setup documentation
    - Visuals or representative output showing the system in operation
    - The flow of data and control through a representative workflow
    - Known compatibility constraints and observed failure modes
    - Design decisions, trade-offs, and links to the relevant concept pages

    Avoid duplicating repository installation instructions or implying that every
    reader should be able to recreate the complete system. The examples are case
    studies of the methodology, not prescribed environments or implementations.

!!! note "The central idea"
    An example succeeds here when it makes the methodology and its reasoning
    understandable. Reproducing the exact hardware, workspace, and software
    environment is optional and is supported by the linked project repositories,
    not by step-by-step instructions in this guide.
