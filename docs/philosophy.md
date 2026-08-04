# Philosophy

Robot manipulation pipelines often combine perception, planning, control, and
other specialized utilities. These capabilities may be coordinated by a state
machine, behavior tree, graphical workflow tool, custom script, or another form of
orchestration.

!!! warning "A core consideration"
    **The choice of orchestrator should not determine whether a useful component
    can participate in the pipeline.**

This methodology therefore treats orchestration and implementation as separate
architectural concerns. The orchestration layer decides **when** work should occur
and owns the clients used to request that work. Modular components decide **how**
the work is performed and expose their capabilities through ROS 2 service or action
servers. Communication then takes place through the ROS 2 interface.

## Motivation

Tightly coupling a utility to one orchestration tool limits where it can be reused.
It can also force teams to adopt unfamiliar tooling before they can benefit from
the underlying capability. A stable ROS 2 interface creates a boundary between
these choices: one team can use FlexBE while another uses MoveIt Pro, OmniGraph,
Simulink, or custom code, without requiring a different implementation of the
utility for each environment.

This separation also allows the two sides to evolve independently. An orchestration
workflow can be reorganized without rewriting the utility, and the utility's
internal library or algorithm can change without redesigning every pipeline that
uses it, provided that its interface contract remains stable.

## Strategy

The strategy is to wrap a focused capability as a ROS 2 component and expose the
operations needed by the rest of the system through explicit interfaces. The
orchestration layer then interacts with that component as a client.

The interface should describe the capability rather than the workflow that happens
to use it. Requests, results, feedback, failure states, timeouts, and cancellation
behavior should be defined at this boundary. This gives any compatible client the
information it needs without embedding higher-level pipeline decisions in the
component itself.

In practical terms, the required interaction helps determine which interface to
use. If a client only needs to send a request, wait for a result, and stop waiting
after a chosen timeout, a ROS 2 [service](ros2-interfaces/services.md) may be enough.
If the work may take longer and the client needs progress feedback or the ability
to cancel it while it is running, a ROS 2 [action](ros2-interfaces/actions.md) is
usually a better fit. Defining those needs explicitly keeps the interface no more
complex than the capability requires.

## Design principles

- Make it clear what each part of the system does, how other parts communicate with
  it, and which part is responsible for each decision.
- Do not make a reusable utility depend on the tool used to coordinate the larger
  workflow.
- Where practical, keep the code that performs the useful work separate from the
  ROS 2 code that communicates with the rest of the system.
- Use the simplest ROS 2 interface that meets the needs of the task.
- Make it possible to tell when work succeeds, fails, or takes too long. When
  appropriate, also make progress, cancellation, and recovery visible.
- Give each component a focused purpose so that it can be built, tested, replaced,
  and reused on its own.
- Treat the examples as illustrations of possible design choices, not as
  requirements to use the same tools.

!!! note "The central idea"
    The orchestration layer owns the clients; modular utilities own the service or
    action servers. As long as both sides honor the ROS 2 interface, an orchestrator
    can be changed without redesigning the utilities, and a utility can be reused
    across pipelines without depending on how those pipelines are coordinated.
