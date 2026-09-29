# SailLink

**Personal telemetry for sailing crews.**

SailLink is a system designed to make onboard information more accessible to every member of a sailing crew.

During sailing or racing, a large amount of useful information is already available through the boat's existing instruments and navigation systems. However, this information is often concentrated on a small number of shared displays.

SailLink creates a **personal information layer** that allows each crew member to access the information that is most relevant to their role through their personal device.

> **One boat, one telemetry stream, personalized information for every crew member.**

---

## What is SailLink?

SailLink connects the information already available onboard with the personal devices used by the crew.

The system receives information from the boat, organizes it into a common format, and makes it available to individual crew members.

Each person can therefore have a different view of the same underlying information.

For example:

* the **helmsman** can focus on information relevant to boat handling;
* the **tactician** can focus on information related to the race situation;
* the **trimmer** can focus on parameters relevant to sail handling;
* the **coach** can have a broader overview of the boat and its performance.

The goal is not to create another navigation system, but to **make existing information more personal and accessible to the crew**.

---

## How it works

At a conceptual level, SailLink connects three elements:

```text
Existing onboard information
             │
             ▼
          SailLink
             │
             ▼
      Crew devices
```

SailLink acts as the layer between the boat's existing information and the people who need to use it.

It collects and organizes the available information and makes it accessible to the crew.

The personal devices can then present the relevant information according to each user's needs.

This keeps three aspects separate:

* the source of the information;
* the distribution and organization of the information;
* the personal experience of each crew member.

---

## Why SailLink?

Modern sailing boats can provide a large amount of information, but not all of it is relevant to everyone onboard.

A single shared display cannot necessarily provide every crew member with **the right information, in the right place, at the right time**.

SailLink addresses this by turning a common information source into a set of personalized experiences.

The value of the system is therefore not simply to display more data, but to **give each person access to the information they actually need**.

---

## Crew Experience

Each crew member can have their own view of the available information.

The same boat can therefore provide a common information source while allowing every smartwatch or personal device to display something different.

This approach makes it possible to adapt the experience to:

* the crew member's role;
* individual preferences;
* the current situation;
* the type of activity;
* the amount of information required.

The interface should also make it immediately clear whether information is current, temporarily unavailable, or if the device is searching for a connection.

---

## A Complementary System

SailLink is designed as a **complement to the boat's existing equipment**.

It is not intended to replace navigation systems, professional onboard instruments, or existing sailing software.

Instead, it provides an additional layer through which crew members can access information that is already available onboard.

SailLink is also not intended to act as a certified navigation or safety device.

---

## Local by Design

SailLink is designed to operate locally within the boat environment.

The core experience does not depend on cloud services or continuous external connectivity.

This allows the system to focus on providing information directly to the crew while they are onboard and sailing.

---

## Project Status

SailLink is currently in the **Proof of Concept and technical validation stage**.

The purpose of this stage is to progressively verify the concept in realistic conditions before moving toward a final product.

The project is focused on demonstrating:

* reliable access to onboard information;
* consistent delivery to crew devices;
* a useful and intuitive crew experience;
* operation with multiple devices;
* reliable behavior during real onboard use;
* suitable power consumption and autonomy;
* sufficient robustness for the intended environment.

Decisions about the final product will be based on the results of this validation phase.

---

## Product Architecture

At a high level, SailLink is composed of several elements working together:

```text
                  SailLink
                     │
          ┌──────────┼──────────┐
          │          │          │
       Onboard     SailLink   Crew
     information    system   devices
          │          │          │
          └──────────┴──────────┘
                     │
              Personal views
```

The architecture is intentionally designed around a simple principle:

> **One shared source of information, multiple personalized experiences.**

The central system should remain independent from the individual roles of the crew, while each personal device determines how the available information is presented.

---

## Development Approach

SailLink is being developed incrementally.

The initial focus is on validating the core concept and the overall user experience.

Only after the main assumptions have been validated will the project move toward more advanced hardware, productization, environmental validation, and broader deployment.

The development process therefore prioritizes:

1. **Concept validation**
2. **Real-world testing**
3. **User experience**
4. **Reliability**
5. **Product refinement**
6. **Industrialization**

The Proof of Concept is not considered the final product. Its purpose is to provide evidence and learning that can guide the next stages of development.

---

## What SailLink Is Not

The initial scope does not include:

* replacing existing navigation systems;
* replacing professional onboard electronics;
* acting as a certified navigation or safety device;
* requiring cloud connectivity during sailing;
* supporting every possible sailing device from the beginning.

The product is intentionally focused on one core use case:

> **Making existing onboard information personally accessible to every member of the crew.**

---

## Vision

The long-term vision of SailLink is to create a flexible information layer for sailing crews.

As the system evolves, the same underlying concept could support different devices, roles, information sources, and sailing environments.

The principle remains the same:

> **The boat generates the information. SailLink makes it personal.**

---

## SailLink in One Sentence

> **SailLink is a local telemetry bridge that turns a boat's existing information into personalized, live information for every crew member.**
