---
layout: post
title: Leaflink - AI Plant Maintenance
image: "/posts/Leaflink.png"
tags: [AI, IoT, LLMs]
---

In the realm of innovative tech solutions for everyday problems, my latest group project (Leaflink) stands out as a testament to the fusion of artificial intelligence and plant care. Leaflink represents a leap forward in how we interact with and maintain our green companions. Here’s a glimpse into how our AI driven plant maintenance system works and what makes it unique.

<a href="https://github.com/JaredLBailey/leaflink" target="_blank">Leaflink GitHub Repo</a>

### Video Overview
[![Leaflink AI Plant Maitenance](https://img.youtube.com/vi/W6LuD98H4Ts/maxresdefault.jpg)](https://www.youtube.com/watch?v=W6LuD98H4Ts)

___

# Table of Contents

- [The Brains Behind Leaflink: Raspberry Pi](#raspberry-pi)
- [Sensors](#sensors)
- [Master and Subordinate Agents](#agents)
- [Voice Interaction](#voice)
- [Technology in Plant Care](#tech)

___

# The Brains Behind Leaflink: Raspberry Pi <a name="raspberry-pi"></a>

At the heart of Leaflink is a Raspberry Pi, which serves as the central processing unit of the entire system. This compact yet powerful device orchestrates all the sensors and actuators, ensuring seamless interaction between various components and effective management of the plant’s environment.

# Sensors <a name="sensors"></a>

Maintaining the ideal environment for plant growth is crucial. Leaflink uses a temperature and humidity sensor to continuously monitor and log these conditions. To provide actionable insights, we incorporated a LangChain agent that performs sophisticated graphing, statistical analysis, and predictive modeling. This allows users to anticipate environmental changes and adjust care routines proactively.

Plants need the right amount of light to thrive. Leaflink addresses this need with a light sensor. When the sensor detects that light levels are too low during datime hours, the system triggers LED lights encircling the plant, mimicking natural sunlight to ensure optimal growth conditions.

The system includes a soil moisture sensor that detects when the soil is too dry. When moisture levels drop below a predetermined threshold, Leaflink activates a motorized water pump to deliver water. This system ensures your plant always has the right hydration.

In addition to watering, Leaflink manages plant nutrition through a motorized plant feeder controlled by a servo motor. This feature ensures that your plant receives regular, measured doses of nutrients, promoting robust growth and vitality.

# Master and Subordinate Agents <a name="agents"></a>

Leaflink employs a master agent to coordinate various lower-level agents. These subordinate agents handle specific tasks such as searching the internet for plant care tips, generating graphs and statistics, and performing retrieval augmented generation (RAG) lookups for detailed plant information. The master agent manages motor controls and interprets voice commands, translating them into JSON directives to operate the system’s components efficiently.

# Voice Interaction <a name="voice"></a>

Interacting with Leaflink is as simple as speaking to it. We’ve integrated a speech-to-text module to facilitate voice commands, making it easy to instruct the system or inquire about plant conditions. To enhance the user experience, we’ve even created a voice clone that mimics my own voice, giving the impression that the plant AI tool is genuinely alive (with its own personality) and engaged in conversation.

# Technology in Plant Care <a name="tech"></a>

Leaflink is more than just a plant maintenance tool. This project represents an advancement in how technology can enhance our interaction with everyday objects. By combining AI, IoT, and voice technology, we’ve created a system that not only simplifies plant care but also makes it more interactive and enjoyable. We’re excited about the potential of Leaflink and look forward to seeing how it evolves.
