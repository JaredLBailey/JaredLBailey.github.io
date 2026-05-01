---
layout: post
title: Walking Flamingo Robot
image: "/posts/glamour_1_1.jpg"
tags: [Design & Build, Simulation, Reinforcement Learning]
---

<p align="center">
  <img src="/img/posts/glamour_1_5.jpg" alt="Finished Robot" title="Finished Robot" width="400">
</p>

For my Robot Studio class project, I designed and built a bipedal flamingo from the ground up. In developing its Duke centric appearance, I incorporated feathers, along with painted eyes and a beak, to give the robot a distinctive visual identity. While the project is technically ambitious, I also wanted it to communicate personality and creativity through its design.

### Video Highlights
[![Flamingo Bipedal Robot](https://img.youtube.com/vi/qqInVzerBGY/maxresdefault.jpg)](https://www.youtube.com/watch?v=qqInVzerBGY)

___

# Table of Contents

- [Technical Pieces](#techincal-pieces)
- [Movement & Simulation](#simulation)
- [AI Concept Video](#ai-video)

___

# Technical Pieces <a name="techincal-pieces"></a>

<p align="center">
  <img src="/img/posts/glamour_1_24.jpg" alt="Acrylic Top" title="Acrylic Top" width="400">
</p>

Standing nearly three feet tall, the robot was developed with both transparency and maintainability in mind. A laser cut acrylic top exposes the internal electronics, allowing viewers to see the computational systems that power the robot. I also designed the platform to be modular, making it easier to replace damaged components, refine individual subsystems, and incorporate future upgrades without requiring a complete redesign.

<p align="center">
  <img src="/img/posts/Explode_2.png" alt="Robot Explosion" title="Robot Explosion" width="400">
</p>

The robot’s hardware includes a Raspberry Pi 4B, an IMU sensor, eight LX-16A motors, and an LCD display that provides simple system-status information. Of the eight motors, six are dedicated to the legs, while the remaining two control expressive motions in the head and tail. This combination allows the robot to function not only as a locomotion platform, but also as a more engaging and character-driven robotic system.

<p align="center">
  <img src="/img/posts/Stack_1.png" alt="Electronics Stack" title="Electronics Stack" width="400">
</p>

___

# Movement & Simulation <a name="simulation"></a>

## Leg Movement Video
<p align="center">
  <a href="https://youtu.be/Cuv5p7rcel4">
    <img src="https://img.youtube.com/vi/Cuv5p7rcel4/hqdefault.jpg" alt="Watch the flamingo robot legs video" width="400">
  </a>
</p>

Before focusing on full body locomotion, I began by exploring the robot’s leg mechanics in isolation. This included testing the initial range of motion and farthest practical extensions of the legs, as well as manually operating both legs while they were still separate from the main body and supported in my hands. These early experiments helped me better understand the robot’s movement limits, joint behavior, and overall mechanical complexity. They also reinforced that, because the legs are such a complex system, effective walking behavior will need to be developed carefully through simulation before being transferred to the physical robot.

I am currently exploring locomotion through simulation in PyBullet before advancing to more consistent walking behavior on the physical robot. This stage is particularly important because the robot uses ball feet, which introduce additional challenges in balance, stability, and control. By developing and testing walking strategies in simulation first, I can evaluate control approaches more efficiently and reduce risk before transferring those ideas to the physical platform.

# AI Concept Video <a name="ai-video"></a>

<p align="center">
  <a href="https://youtube.com/shorts/V0wq_how2O0">
    <img src="https://img.youtube.com/vi/V0wq_how2O0/hqdefault.jpg" alt="Watch the flamingo robot concept video" width="400">
  </a>
</p>

I am also including an AI generated video depicting the robot walking. This video is intended as a conceptual demonstration of the project’s direction rather than documentation of the robot’s present physical capabilities. Including it helps illustrate the longer-term vision for the platform.
