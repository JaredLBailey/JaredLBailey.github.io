---
layout: post
title: Duke Robotics Club - Robot Submarine
image: "/posts/wheres-waldo.jpg"
tags: [Robotics]
---

Being part of the Duke Robotics team throughout 2024 has been an extraordinary journey filled with excitement and challenges. This year we achieved a remarkable 8th place (out of 41 teams) at the international competition, our highest ranking in 15 years. We also faced an unexpected setback when our robot was flooded during a pool test a few months before competition, leading to a complete rebuild of the electronics. In the following sections, I’ll delve into the details of my contributions and experiences with the team this year.

<a href="https://www.duke-robotics.com" target="_blank">Duke Robotics Club Website</a>

### 2023-2024 Season Video Highlights
[![2024 Robotics Season Overview](https://img.youtube.com/vi/hP1Sr-XBpaE/maxresdefault.jpg)](https://www.youtube.com/watch?v=hP1Sr-XBpaE)

___

# Table of Contents

- [Navigating the Acoustics Challenges](#acoustics-challenges)
- [Modeling and Evaluation](#modeling-evaluation)
  - [Model Misses](#model-misses)
- [Learnings](#learnings)

___

# Navigating the Acoustics Challenges <a name="acoustics-challenges"></a>


Joining the Electrical team at Duke Robotics opened the door to an intriguing challenge: improving our robot’s acoustic navigation system. The core problem was that during competition, our robot had to autonomously locate a pinger submerged in a pool. This task proved to be more difficult than anticipated because the water environment distorted the acoustic signals, making it hard for the robot to clearly detect the pinger.

When I came on board, the acoustics project was already behind schedule, with two previous teams having tried and moved on to other areas. Our system at that time utilized three hydrophones positioned on the sides of the robot. The strategy was to determine the pinger’s direction by analyzing which hydrophone received the ping first, second, and third. We then hoped to use this data to identify the correct directional octant.

My initial approach involved developing a neural network with another team member to analyze this data. Unfortunately, our model’s accuracy was only 60%, which wasn’t sufficient for reliable performance. A deeper dive into the data revealed two major issues: first, some data was corrupted by recordings taken outside the pool, and second, the side-mounted hydrophones were experiencing difficulties from the sound signal interaction with the robot’s structure.

To address these issues, I proposed a new system featuring four hydrophones arranged in a square formation, with each hydrophone positioned just 2 inches apart. This new setup allowed us to place the hydrophones lower on the robot, reducing interference from the robot’s body and the thrusters. By utilizing this four-hydrophone array, we eliminated the need for complex neural network processing. Instead, we could direct the robot to move towards the hydrophone that detected the ping first, streamlining the navigation process.

This approach not only had the promise of improving the robot’s accuracy in detecting the pinger but also brought us back on track with our project timeline. But just before we were able to test the new design, disaster struck.

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

