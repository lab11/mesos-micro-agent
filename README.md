Mesos Micro Agent
=================

The Mesos Micro Agent intends to extend the resource management, execution, and
containerization functions of Mesos to very resource constrained computers, 
many of which will not be running on traditional operating systems.

## Motivation

Traditionally, resource constrained computers are programmed with single-purpose
embedded applications, however scenarios such as the collection and processing of
sensor data, the contextual repurposing of sensing and compute, and the ability
of multiple parties to contribute to the control of embedded actuators call for
more dynamic applications running in a multi-tenant environment on the sensor node.

To enable this vision we take inspiration of cloud computing frameworks,
and attempt to create a resource manager and execution environment that would 
allow the dynamic utilization of the compute, memory, networking, and sensing
resources available on these devices.

Mesos is the closest existing resource manager to accomplishing these goals due to
its already small (but not small enough) memory footprint, relatively minimal
internal protocols, and acceptance of custom resource types and attributes which will be present
on these devices but are not present in today's cloud.

## High level architecture

TODO: Picture

The Mesos Micro Agent will appear to the Mesos master as a fully functioning
mesos agent. This will be accomplished through the proxying of resource constrained
networking protocols, and potentially the proxying of low-latency actions
by a cloud-based agent component.

The Mesos Micro Agent will also rethink the executor component of the mesos
agent, and will probably required several different default executors to 
successfully execute in non \*nix environments. This could mean the execution
of raw binaries on the target architecture, but hopefully will instead be the use
of WASM or some other efficient, sandboxed runtime.

## Implementation Details

This is a rust project because it is perhaps the only logical language choice
for creating a new project that runs on a variety of platforms, including bare metal.

The software is split into two components: a core code base which implements
the Mesos protocol, and an OS (or hardware) abstraction layer which allows
the agent to retrieve available resources, spawn executors, and perform networking
functions. The abstraction layer would need to be implemented for every new target.
