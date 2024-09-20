---
layout: post
title: Ongoing - AI Garden Pest Deterrent
image: "/posts/Bird_1.jpg"
tags: [3D Printing, Computer Vision, Raspberry Pi, Docker, AWS]
---

In my ongoing quest to combine AI with practical applications, I’ve embarked on v2 of a project that builds on the foundation of a team effort from my Deep Learning Applications class. The original team project (v1) used computer vision to identify whether an image contained a bird or a squirrel, with a Raspberry Pi triggering an ultrasonic sound to deter squirrels from a bird feeder. In this updated version, I individually aim to push the boundaries of what the project can achieve by introducing more advanced features and further refining the detection capabilities.

<a href="https://github.com/JaredLBailey/wheres-waldo" target="_blank">Version 1 - GitHub Repository</a>




___

# Table of Contents

- [Version 1](#version-1)
  - [The System](#system)
  - [Build in Progress](#build-in-progress)
- [Version 2](#version-2)
  - [Model Misses](#model-misses)
- [Learnings](#learnings)

___

# Version 1 <a name="version-1"></a>

In version 1, our team set out to create an automated system that could distinguish between birds and squirrels to humanely deter the latter from bird feeders. 

### The System <a name="system"></a>

![alt text](/img/posts/Bird_2.jpg "Version 1 Build System")

The system began with an IR sensor that detected movement, triggering a day and night sensitive camera to capture a photo. This image was then sent via API to the cloud, where a custom image classifier determined if the subject was a bird or a squirrel. If a squirrel was detected, a response message was sent back to a Raspberry Pi, which activated a relay switch plugged into a wall outlet. This powered AA batteries, which we converted to C batteries that ran a commercially available pest repellent to ward off the squirrels.

### Build in Progress <a name="build-in-progress"></a>

![alt text](/img/posts/Bird_3.png "Jay Hard at Work")

For this project, I was assigned to handle the hardware. I designed and built the electronics system that powered the pest repellent, including wiring the relay and battery conversions. Meanwhile, my teammate Jay took on the task of building a balsa wood box to house and protect the electronics. You can see a photo of Jay hard at work on the enclosure, which completed the system’s design.

___

# Modeling and Evaluation <a name="modeling-evaluation"></a>

For the modeling phase of this project, I utilized YOLOv8, Python, and the Ultralytics library to tackle the challenge of detecting all five characters simultaneously. I experimented with two distinct approaches to determine the most effective strategy for character identification. The first approach focused on detecting only the heads of the characters, under the assumption that the heads would be less obstructed in the photos despite being smaller in size. The second approach aimed to detect the full characters, which provided a larger target but was often hindered by obstructions and varying image conditions. By comparing these methods, I evaluated whether the advantage of larger size outweighed the difficulties posed by obstructions. Ultimately, the head-only model proved to be more successful, yielding superior results and more accurate detections. This approach balanced the trade-off between size and visibility, demonstrating that, in this case, focusing on less obstructed, though smaller, features led to better overall performance.

![alt text](/img/posts/waldo-evaluation.png "Model Evaluation")

### Model Misses <a name="model-misses"></a>

Model misses were an inevitable part of this project, highlighting the challenges inherent in object detection. 

For example, in the two photos on the left, the characters have hairstyles and large eyes that resemble Waldo and Odlaw, leading the model to incorrectly identify them based on these features. Additionally, the lower character’s teeth were mistaken for Odlaw’s mustache. 

The top middle photo features an object with a shape and color similar to the wizard’s hat, which confused the model. The bottom middle photo is the wizard himself, whose recognition was hampered by heavy obstruction from surrounding elements. 

The lower right photo, showing Woof's tail, presented difficulties due to his small size and low pixel count, making accurate detection challenging. The upper right photo is actually a shirt sleeve that resembles Woof's tail, further complicating the model’s ability to distinguish between the character and non-character elements. 

These misses underscore the need for continued refinement in object detection models to handle diverse and obstructed visual information effectively.

![alt text](/img/posts/waldo-model-miss.png "Model Miss")

___

# Learnings <a name="learnings"></a>

This project provided valuable insights into the performance of YOLOv8 for detecting characters in the "Where's Waldo?" series, revealing important nuances in object detection. Different characters exhibited varying levels of precision and recall, influenced largely by their shapes and the nature of their surroundings. For instance, Woof’s tail was often unobstructed, which contributed to high precision, but Woof’s small size led to lower recall rates as the model struggled with detecting such small features.

The project also demonstrated the capabilities and limitations of small object detection. The model effectively identified objects as small as 20x20 pixels, but background noise, imperfect photo conditions, and object obfuscation meant that achieving reliable results generally required objects to be around 50x50 pixels. This highlights the trade-offs involved in balancing object size and detection accuracy.

Tiling images emerged as a crucial technique for this project, allowing for detailed analysis without rescaling, which could lead to loss of critical information. Although overlapping tiles by 40 pixels helped mitigate information loss, challenges persisted, such as cutting off faces at the edges of tiles. These experiences underscore the importance of fine-tuning both data preprocessing methods and model parameters to enhance detection performance in practical applications.
