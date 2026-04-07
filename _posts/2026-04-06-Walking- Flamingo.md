---
layout: post
title: Walking Bipedal Robot
image: "/posts/glamour_1_1.jpg"
tags: [Design & Build, Simulation, Reinforcement Learning]
---

For my Robot Studio class project, I designed and built a bipedal flamingo from the ground up. In developing its Duke centric appearance, I incorporated feathers, along with painted eyes and a beak, to give the robot a distinctive visual identity. While the project is technically ambitious, I also wanted it to communicate personality and creativity through its design.

___

# Table of Contents

- [Technical Pieces](#techincal-pieces)
- [Simulation](#simulation)
- [AI Video](#ai-video)

___

# Technical Pieces <a name="techincal-pieces"></a>

Standing nearly three feet tall, the robot was developed with both transparency and maintainability in mind. A laser cut acrylic top exposes the internal electronics, allowing viewers to see the computational systems that power the robot. I also designed the platform to be modular, making it easier to replace damaged components, refine individual subsystems, and incorporate future upgrades without requiring a complete redesign.

The robot’s hardware includes a Raspberry Pi 4B, an IMU sensor, eight LX-16A motors, and an LCD display that provides simple system-status information. Of the eight motors, six are dedicated to the legs, while the remaining two control expressive motions in the head and tail. This combination allows the robot to function not only as a locomotion platform, but also as a more engaging and character-driven robotic system.

___

# Simulation <a name="simulation"></a>

I am currently exploring locomotion through simulation in PyBullet before advancing to more consistent walking behavior on the physical robot. This stage is particularly important because the robot uses ball feet, which introduce additional challenges in balance, stability, and control. By developing and testing walking strategies in simulation first, I can evaluate control approaches more efficiently and reduce risk before transferring those ideas to the physical platform.

# AI Video <a name="ai-video"></a>

I am also including an AI generated video depicting the robot walking. This video is intended as a conceptual demonstration of the project’s direction rather than documentation of the robot’s present physical capabilities. Including it helps illustrate the longer-term vision for the platform.
