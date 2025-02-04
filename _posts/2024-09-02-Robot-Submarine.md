---
layout: post
title: Duke Robotics Club - Robot Submarine
image: "/posts/cropped-Master_Robosub_AllDaysAllTeams-26-scaled-1.jpg"
tags: [Robotics]
---

Being part of the Duke Robotics team throughout 2024 has been an extraordinary journey filled with excitement and challenges. This year we achieved a remarkable 8th place (out of 41 teams) at the international competition, our highest ranking in 15 years. We also faced an unexpected setback when our robot was flooded during a pool test a few months before competition, leading to a complete rebuild of the electronics. In the following sections, I’ll delve into the details of my contributions and experiences with the team.

<a href="https://www.duke-robotics.com" target="_blank">Duke Robotics Club Website</a>

### 2023-2024 Season Video Highlights
[![2024 Robotics Season Overview](https://img.youtube.com/vi/hP1Sr-XBpaE/maxresdefault.jpg)](https://www.youtube.com/watch?v=hP1Sr-XBpaE)

___

# Table of Contents

- [Upcoming Year](#upcoming-year)
  - [ROS 2 Migration](#ros2-migration)
- [Last Year](#last-year)
  - [Can you Hear Me Now?: Navigating the Acoustics Challenges](#acoustics-challenges)
  - [A Setback and Rebuild: The Unexpected Challenge](#setback-rebuild)
  - [Diving into the Deep End: A Summer of Pool Tests](#pool-tests)
  - [Thankful](#thankful)

# This Year <a name="upcoming-year"></a>

___

### ROS 2 Migration <a name="ros2-migration"></a>

For this year I've transitioned from the Electrical Team to the Computer Science Team. As ROS 1 is set to be depricated in 2025, I worked to update our Python and C++ code from ROS 1 to ROS 2. This involved a ton of updates and testing to the 50,000+ lines of code in our repository. I spent most of my time in the task planning and utilities sections of our code base, but did do some branching out to other areas as called for (sonar, CV, etc.). And once this was done, I spent a couple weeks linting.

Now I've moved to testing the ROS 2 code using a Jetson Orin Nano on a mock electrical circuit assembled by the Electrical team. This included setting up the Nano.

___

# Last Year <a name="last-year"></a>

___

### Can you Hear Me Now?: Navigating the Acoustics Challenges <a name="acoustics-challenges"></a>


Joining the Electrical team at Duke Robotics opened the door to an intriguing challenge: improving our robot’s acoustic navigation system. The core problem was that during competition, our robot had to autonomously locate a pinger submerged in a pool. This task proved to be more difficult than anticipated because the water environment distorted the acoustic signals, making it hard for the robot to clearly detect the pinger.

When I came on board, the acoustics project was already behind schedule, with two previous teams having tried and moved on to other areas. Our system at that time utilized three hydrophones positioned on the sides of the robot. The strategy was to determine the pinger’s direction by analyzing which hydrophone received the ping first, second, and third. We then hoped to use this data to identify the correct directional octant. The data was complex since pings come in waves. We isolated the true from false signals by honing in on when the sound wave eclipsed 5 standard deviations from the mean (the upper and lower most horizontal red lines).

![alt text](/img/posts/Screenshot-2024-02-29-194412.png "Acoustics Data")

My initial approach involved developing a neural network with another team member to analyze this data. Unfortunately, our model’s accuracy was only 60%, which wasn’t sufficient for reliable performance. A deeper dive into the data revealed two major issues: first, some data was corrupted by recordings taken outside the pool, and second, the side-mounted hydrophones were experiencing difficulties from the sound signal interaction with the robot’s structure.

To address these issues, I proposed a new system featuring four hydrophones arranged in a square formation, with each hydrophone positioned just 2 inches apart. This new setup allowed us to place the hydrophones lower on the robot, reducing interference from the robot’s body and the thrusters. By utilizing this four-hydrophone array, we eliminated the need for complex neural network processing. Instead, we could direct the robot to move towards the hydrophone that detected the ping first, streamlining the navigation process.

This approach not only had the promise of improving the robot’s accuracy in detecting the pinger but also brought us back on track with our project timeline. But just before we were able to test the new design, disaster struck.

___

### A Setback and Rebuild: The Unexpected Challenge <a name="setback-rebuild"></a>

During a routine pool test, the robot was accidentally flooded. This unforeseen mishap forced us to put a halt on the acoustics project and shift our focus to a crucial rebuild of the robot’s electrical system. The flood had damaged several key components, leaving the entire electrical team with the monumental task of repairing and restoring the robot’s functions. Despite the setback, we had a sense of humor about the situation and played the Tintanic movie theme song throughout our next meeting.

I threw myself into the rebuilding process, which involved extensive rewiring and testing. One of my key responsibilities was to address the issues with our Electronic Speed Controllers (ESCs) for the thrusters. As part of the team I rewired, soldered, and performed lots of tests. Once this task was complete I spent hours connecting wires, applying epoxy to seal connections, and organizing the wiring within the robot’s sealed capsule to maximize space and functionality.

The rebuild was a complex and time-consuming task. It took our team nearly two months of hard work and dedication to complete. Despite the setbacks, the extensive effort paid off. Once the robot was reassembled and thoroughly tested, it was not only functional again but performed better than before.

___

### Diving into the Deep End: A Summer of Pool Tests <a name="pool-tests"></a>

With the robot back in top shape, I eagerly volunteered to spend my summer immersed in pool tests. Each day, my responsibilities included building and setting up various obstacles in the pool, as well as swimming alongside as the robot navigated them successfully. I also took on the crucial task of keeping the robot away from the pool’s walls and other swim lanes, managing its transportation to and from the pool, and rigorously checking its water-tightness before each test.

Aside from these manual duties, I provided valuable feedback to the Computer Science team about the robot's performance. This feedback loop was essential for fine-tuning the robot's behavior and improving its autonomous navigation capabilities. Additionally, I filmed underwater footage for the club's promotional videos, capturing the robot’s progress and our team's hard work.

The summer’s efforts bore fruit when, for the first time in years, we successfully completed an autonomous pre-trial competition run midway through the season. This milestone was a testament to the dedication of our team and the significant progress we had made.

Among the many moments of that summer, one particularly memorable event stands out. One day, a fellow team member accidentally dropped a 40-pound weight into the 17-foot deep diving pool. The weight sank quickly to the bottom, and with a bit of determination, I took on the challenge of retrieving it. To everyone’s amazement, I swam down and brought the weight back up on my first try. The lifeguards watching from the poolside were visibly impressed, adding an unexpected highlight to our summer.

___

### Thankful <a name="thankful"></a>

This year's experience was more than just a series of technical tests; it was a season of camaraderie, problem-solving, and personal achievement. The hard work and dedication not only advanced our robot’s capabilities but also deepened my connection with the team and the project. I am grateful for the opportunities provided and the season ahead.

