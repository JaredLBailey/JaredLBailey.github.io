---
layout: post
title: Ongoing - AI Garden Pest Deterrent
image: "/posts/Squirrel_1.png"
tags: [Fushion360, 3D Printing, Computer Vision, Raspberry Pi, Docker, AWS]
---

In my ongoing quest to combine AI with practical applications, I’ve embarked on v2 of a project that builds on the foundation of a team effort from my Deep Learning Applications class. The original team project (v1) used computer vision to identify whether an image contained a bird or a squirrel, with a Raspberry Pi triggering an ultrasonic sound to deter squirrels from a bird feeder. In this updated version, I individually aim to push the boundaries of what the project can achieve by introducing more advanced features and further refining the detection capabilities.

<a href="https://github.com/JaredLBailey/wheres-waldo" target="_blank">Version 1 - GitHub Repository</a>

___

# Table of Contents

- [Version 1](#version-1)
  - [The System](#system)
  - [Build in Progress](#build-in-progress)
- [Version 2](#version-2)

___

# Version 1 <a name="version-1"></a>

In version 1, our team set out to create an automated system that could distinguish between birds and squirrels to humanely deter the latter from bird feeders. 

### The System <a name="system"></a>

![alt text](/img/posts/Bird_3.png "Version 1 Build System")

The system began with an IR sensor that detected movement, triggering a day and night sensitive camera to capture a photo. This image was then sent via API to the cloud, where a custom image classifier determined if the subject was a bird or a squirrel. If a squirrel was detected, a response message was sent back to a Raspberry Pi, which activated a relay switch plugged into a wall outlet. This powered AA batteries, which we converted to C batteries that ran a commercially available pest repellent to ward off the squirrels.

### Build in Progress <a name="build-in-progress"></a>

![alt text](/img/posts/Bird_2.jpg "Jay Hard at Work")

For this project, I was assigned to handle the hardware. I designed and built the electronics system that powered the pest repellent, including wiring the relay and battery conversions. Meanwhile, my teammate Jay took on the task of building a balsa wood box to house and protect the electronics. You can see a photo of Jay hard at work on the enclosure, which completed the system’s design.

___

# Version 2 <a name="version-2"></a>

For version 2 of this project, I decided to go solo with my team’s blessing, aiming to enhance the system for practical use in gardens. I streamlined the hardware and software, reducing the system’s complexity while expanding its functionality. To achieve a more polished and durable design, I learned Fusion360 and used it to create a custom 3D-printed case for the electronics, which not only improved the system's appearance but also made it more weather-resistant.

The key upgrade for version 2 is a 12-animal object detection model hosted in the cloud, allowing for more precise identification of garden intruders. In addition to improving the detection capabilities, I also wired a waterproof ultrasonic speaker to ensure the system can function outdoors in various conditions. Below, you’ll find photos of the 3D-printed case, both from Fusion360 and in real life, showcasing the physical evolution of the project.

![alt text](/img/posts/Bird_1.jpg "3D Print")
![alt text](/img/posts/Bird_4.png "Fushion360")
