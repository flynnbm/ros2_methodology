# ROS 2 Interfaces

ROS 2 provides several ways for components to communicate. Although more than one
approach can often be made to work, there is usually one that expresses the
interaction more clearly and with less unnecessary machinery. The goal is to use
the simplest interface that provides the behavior the component actually needs.

ROS 2 officially groups these approaches as
[topics, services, and actions](https://docs.ros.org/en/jazzy/Concepts/Basic/Interfaces-Topics-Services-Actions.html).
This section focuses on selecting among those interface types based on how
components need to interact.

The first distinction is between a stream of information and a request to perform
work. [Publishers](publishers.md) and [subscribers](subscribers.md) communicate
through topics, which are well suited to ongoing data and events. [Services](services.md)
and [actions](actions.md) connect a specific request to a response or result, which
makes them better suited to operations initiated by a client.

## Choosing an interface

Start by asking what the client needs to know:

- Is information produced continuously or whenever it becomes available?
- Is a response required for a specific request?
- Could the work take long enough that progress feedback would be useful?
- Must the client be able to cancel work that is already running?
- Does the information need to go to one place, or should several parts of the
  system be able to receive it?

The answers generally lead to the following choices:

!!! info "Explore the interface types"
    Compare what each interface is good at, where it falls short, and what to use
    instead. If the full table is not visible, scroll horizontally to see the
    remaining columns.

| Interface | Communication style | What it is good at | What it is not good at | Consider instead |
| --- | --- | --- | --- | --- |
| **Topic: [publisher](publishers.md) and [subscriber](subscribers.md)** | One-to-many asynchronous stream | Continuous sensor data, state updates, and events with loose coupling | Connecting a request to its result, confirming that work completed, or providing built-in cancellation | Use a **service** for a short request and response, or an **action** for longer goal-oriented work |
| **[Service](services.md)** | One-to-one request/response | A bounded request that returns one response, especially when the work is quick and the client can apply a timeout | Long or unpredictable work, progress updates, and canceling work already in progress | Use an **action** when the client needs feedback or cancellation; use a **topic** for an ongoing stream |
| **[Action](actions.md)** | One-to-one asynchronous goal, feedback, and result | Goal-oriented work that may take time and needs a result, progress feedback, or cancellation | Simple lookups and quick operations where goal management adds unnecessary complexity; continuous data streams | Use a **service** for a simple request and response, or a **topic** for continuously produced data |

A subscriber can receive progress-like messages without blocking, but a topic does
not by itself connect those messages to a particular request like with a service, or provide the goal,
result, and cancellation behavior of an action.

## Brief examples

- A camera continuously publishing images and depth data is a natural fit for a
  topic, with any interested components acting as subscribers.
- A client requesting a quick calculation and waiting for one result may only need
  a service.
- A client requesting robot motion or another longer operation may need an action
  so that it can monitor progress, receive the final result, and cancel safely.
- A one-way command may fit a topic when no confirmation is needed. If the client
  must know whether the command was accepted or completed, a service or action
  expresses that requirement more clearly.

## Interface guidance and complete examples

The pages in this section briefly explain how to create each interface and identify
the decisions that matter when using it. They are intended as focused references,
with links to the corresponding official ROS 2 documentation.

The [Examples](../examples/index.md) section is reserved for complete integrations.
Those pages can show how an interface is used by a real component, explain why it
was selected, and cover configuration, execution, results, and failure handling in
the context of a working pipeline.

!!! note "The central idea"
    Choose the least complex interface that still represents the interaction.
    Use topics for streams and events, services for short request/response
    work, and actions when a goal needs feedback, cancellation, or a result after
    longer-running work.
