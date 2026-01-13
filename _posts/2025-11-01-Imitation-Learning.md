---
layout: post
title: Page in Progress - Creative Tool Use
image: "/posts/RobotArm_0.jpg"
tags: [Imitation Learning, State Machine Framework, Creative Tool Use, Robot Learning]
---

# Page in Progress, Please Excuse the Mess

This project explores creative tool use in robotics: training a robot arm to both position and cut a food item using a single tool - a pair of scissors mounted on a custom end effector.

Traditionally, a robot would solve this by swapping tools: pick-and-place to reposition the object, then switch to a cutting tool. That process adds time, complexity, and failure points. Here, the robot instead treats the scissors as a multi-purpose tool to:
- Position: guide and orient the food item using both scissor blades
- Cut: execute the final slicing motion once aligned

To make the full workflow autonomous and robust, I built a State Machine Framework (SMF) and trained two custom YOLO classification models to verify completion between subtasks. When a failure is detected, the SMF automatically retries earlier states to recover and continue.

### Full Project Details and Code
- <a href="https://github.com/JaredBaileyDuke/creative-tool-use/" target="_blank">Creative Tool Use GitHub Repo</a>

___

# Table of Contents

- [System Design](#system-design)
- [Project Phases](#project-phases)
- [Checkers Game](#checkers)

___

# System Design <a name="system-design"></a>

At a high level, the system is built around three ideas:
1) One tool, two roles
The scissors act as both:
- a manipulation surface (pushing/guiding with blades)
- a cutting mechanism (closing motion once aligned)
2) Task decomposition into stable subtasks
Rather than training one policy to “do everything,” the pipeline breaks the job into reliable subtasks, each with its own data + policy.
3) Autonomous verification + recovery
Instead of relying on a human to say “yep, that worked,” the pipeline uses YOLO classification to check progress and automatically retry when things go wrong.

___

# Project Phases <a name="project-phases"></a>
## Phase 1 — Initial Exploration (Franka Research 3)
This phase was about feasibility: can a robot operate a one-degree-of-freedom tool (scissors, pliers, can opener) as part of an imitation-learning pipeline?

I designed a modified snap-click end effector to mount a standard pair of scissors to the robot wrist. The mount needed to:
- align cleanly to the wrist connector
- hold the scissors in place while allowing rotation in the handle holes
- allow the arm’s finger motion to open/close the handles

## Phase 2 — Pick and Place Exploration (SO-101 + LeRobot)
This stage moved onto the LeRobot SO-101 leader–follower system and focused on building a clean imitation learning workflow using:
- leader teleoperation for demonstrations
- ACT (Action Chunking Transformer) policies for learning
- synchronized multi-camera observations

The robot repeatedly followed a trajectory that looked right but missed the grasp by just enough to fail. That pointed to a core truth: Data quality beat model choice. This required several changes:
- improved camera angles (less occlusion, more task visibility)
- stabilized mounts (less shake / blur)
- better lighting (less glare and shadow)
- higher-contrast objects (for easier viewing)
- less variation in data collection (help convergence)
- more episodes (increase examples to learn from) 

With a sterile setup and an intentionally overfit training run, the robot performed consistent pick-and-place.

## Phase 3 — Final Deployment (Creative Scissors Pipeline)
This stage integrated everything into a functioning multi-step system: position + cut a food item using scissors on the SO-101.

Custom Scissors End Effector

The snap-click scissors mount performed well at full size, but at smaller scale snap connections became mechanically unreliable. I solved this practically with superglue + color-matched duct tape, keeping the tool stable for repeated runs.

Subtask performance

Push-only: reliable linear pushing, occasional rolling due to the object

Cutting: consistent once inside a defined target region; occasional “over-eager” repeated cuts






# Computer Vision <a name="cv"></a>
![alt text](/img/posts/CV_0.jpg "Computer Vision")

The computer vision integration allows for ease in the robot recognizing human moves. Video capture permits for the game memory to be updated with the current board state layout.

The computer vision module utilizes a live video feed from a camera on a stand that is detached from the board. The decision to detach the camera and stand was due to robot storage space limitations. This detachment presents an additional difficulty of allowing for a variety of camera locations and rotations in relation to the board. The difficulty creates the need for capture of not only piece locations, but also board location and orientation. This was accomplished using 4 AprilTags, where only 3 are required and the last is present for redundancy.

An HSV filter with contour detection is combined with the known board orientation to identify piece color, location, and king status.

# Animatronics & Voice Clone <a name="animatronics"></a>
![Animatronic Eyes](https://raw.githubusercontent.com/JaredLBailey/JaredLBailey.github.io/master/img/posts/Eyes-0.gif)

STL files were obtained from Will Cogley (<a href="https://willcogley.notion.site/Will-Cogley-Project-Archive-75a4864d73ab4361ab26cabaadaec33a" target="_blank">animatronic eyes</a>) and Fanki the Printer (<a href="https://makerworld.com/en/models/657234#profileId-584358" target="_blank">model of daughter's teeth</a>). The printed output from Will’s STL files did not fit properly, due to many issues with tolerances. This required multiple adjustments and reprints for proper function. The teeth mold was not designed for animatronic use, and was modified to allow for the desired movement by my teammate Kaelyn.

The animatronics were controlled using an arduino and serial communication for mouth movement in order to sync with the voice clone.

Kent Yamamoto provided the voice for our robot. I recorded samples of Kent speaking complex sentences containing a large variety of English phonemes in various positions within words and sentences, capturing the required parts of speech to effectively mimic natural language. I also recorded Kent speaking fluidly using intuitive speech, so that our cloned voice would have a realistic feel.

With the cloned voice I produced over 50 prerecorded sayings. Additionally the voice can be accessed through API by calling a Local LLM (Llamafile) or ChatGPT, and ElevenLabs for live and novel interaction.

# Checkers Game <a name="checkers"></a>
### Video Preview - Robot vs Human
[![Human Plays Robot](https://img.youtube.com/vi/cr42X2ZvtG8/sddefault.jpg)](https://www.youtube.com/watch?v=cr42X2ZvtG8&t)

The game was built using Object Oriented Programming. Classes were created for the piece, board, and game. The piece class contained information about and methods concerning the location, color, king status, etc. The board class contained information about and methods concerning the available movements, current board layout, etc. The game class contained play for the human, random, prioritize jumps, LLM, and minimax actors.

My teammates designed and printed a custom end effector to hold an electromagnet, which in turn can pick up the pieces. I connected the electromagnet to a relay, and wrote code to have it seemlessly operate with the robot arm movements. The end effector makes use of an 8V electromagnet controlled by a 5V wired relay.

While playing checkers, there are four main actions the robot can perform. The robot can move a piece from one square to the next, move a piece off the board after a jump or kinging occurs, add a king to the board, or move out of the way to allow a human turn without obstruction. Motion and path planning is integrated with other parts or the robotic system (electromagnet, voice clone, animatronics, and camera) to allow for proper operation of the entire robot. As an added bonus, we worked to integrate voice commands to control the robot movement.
