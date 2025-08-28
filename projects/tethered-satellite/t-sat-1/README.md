---
description: Explanation of the T-Sat-1 mission plan, goals, and architecture.
---

# T-Sat-1

Tethered-Sat-1 (T-Sat-1) was the Knights Satellite Club’s second balloon-based CubeSat mission and the direct successor to [T-Sat-0](../t-sat-0/). The goal of this mission was not to introduce a new experiment but to refine and validate the systems first flown on T-Sat-0. Lessons learned from the initial mission directly shaped the design, software, and operations of T-Sat-1, ultimately resulting in a smoother flight and a successful parachute deployment at the correct altitude.

Where T-Sat-0 served as a proof of concept, T-Sat-1 demonstrated maturity. The most important change was the elimination of accelerometer based freefall detection, which in the past had caused premature parachute deployments. For T-Sat-1, the [software](software.md) was restructured to rely solely on barometric altitude readings, ensuring the parachute deployed only once the payload crossed the programmed altitude threshold in true free fall. This improvement greatly increased mission reliability.

The mission showed that an iterative, semester to semester development process works. Deployment, housing, and operational issues identified during T-Sat-0 were directly addressed in T-Sat-1. As a result, the payload completed a clean ascent under the weather balloon, separated successfully using the burnwire system, and deployed its parachute exactly as planned. This can be seen in the [flight results](flight-results.md).

Key objectives of T-Sat-1 included:

* Validating usability improvements to mechanical components.
* Proving the effectiveness of barometric only deployment logic.
* Improving launch day operations through better planning, tools, and hardware usability.
* Continuing to develop rapid turnaround workflows for new member training.

By achieving these goals, T-Sat-1 refined the tethered balloon platform and solidified the T-Sat program as a dependable test bed for subsystem validation and hands-on training.
