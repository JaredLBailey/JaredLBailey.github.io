---
layout: post
title: Finding Waldo and His Friends with Computer Vision
image: "/posts/wheres-waldo.jpeg"
tags: [YOLO, Machine Learning, AI, Computer Vision, Python]
---

Welcome to my nostalgia project, where I delve into a fascinating task that blends childhood memories with cutting-edge technology. In this post, I’ll walk you through the creation of a machine learning model designed to tackle a unique challenge: finding Waldo and his four friends (Wenda, Wizard, Odlaw, and Woof) in the iconic "Where's Waldo?" series using YOLOv8. This project not only highlights the power of advanced object detection but also celebrates the playful challenge of spotting hidden characters in a sea of visual complexity. Join me as I explore the intricacies of training YOLOv8 for this whimsical quest and share insights into how modern machine learning can bring classic characters into the digital age.

The primary goal of this project was to create a practical tool that leverages machine learning to simplify the classic "Where's Waldo?" experience. By developing a YOLOv8-based model, I aimed to enable users to take a photo of a book page with their cell phone and have it automatically identify Waldo and his four friends in real time. This functionality not only enhances the interactive enjoyment of the "Where's Waldo?" series but also demonstrates how advanced object detection can be applied to everyday tasks. The vision was to make character identification effortless and immediate, turning a challenging visual puzzle into a seamlessly integrated digital experience.

This project extends beyond the playful realm of "Where's Waldo?" to address critical challenges in the field of small object detection, which is crucial for technologies like self-driving cars and drones. Detecting small or partially obscured objects in real-time is a common hurdle in these applications, where precision and speed are paramount. The techniques refined during this project, such as focusing on less obstructed features and managing varying image conditions, are directly applicable to these domains. For self-driving cars, this means improved detection of pedestrians, cyclists, and other small hazards, while for drones, it enhances the ability to identify and track small objects or obstacles in dynamic environments. By addressing the complexities of small object detection in a controlled setting, this project provides valuable insights and methodologies that can be adapted to improve the robustness and accuracy of object detection systems in more complex, real-world scenarios.

<a href="https://huggingface.co/spaces/JaredBailey/WheresWaldo" target="_blank">Application</a>

<a href="https://github.com/JaredLBailey/wheres-waldo" target="_blank">GitHub Repository</a>

![alt text](/img/posts/small-object-detection-applications.png "Small Object Detection Applications")


# Table of Contents

- [Data Gathering](#data-gathering)
- [Modeling and Evaluation](#modeling-evaluation)
- [Linear Regression](#linreg-title)
- [Decision Tree](#regtree-title)
- [Random Forest](#rf-title)
- [Modeling Summary](#modelling-summary)
- [Predicting Missing Loyalty Scores](#modelling-predictions)
- [Growth & Next Steps](#growth-next-steps)

___

# Data Gathering <a name="data-gathering"></a>


Data gathering for this project presented unique challenges due to the need to account for the imperfect conditions of real-world photographs taken with a cell phone. Many of the existing datasets I found online featured ideal conditions—perfect lighting, flat pages, and high resolution—which didn't accurately reflect the varied conditions one might encounter with a typical cell phone camera. To address this, I created my own dataset using my iPhone, capturing photos of full puzzle pages. Initially, this approach proved problematic because the model struggled with the low resolution of these images, particularly given the small size of Waldo. To improve performance, I refined my data collection strategy by focusing on single page photos, which I then divided into 640 by 640 pixel tiles with slight overlaps. This adjustment allowed the model to better handle the resolution and intricacies of the task, leading to more accurate and effective character detection.

---

### Modeling and Evaluation <a name="modeling-evaluation"></a>

For the modeling phase of this project, I utilized YOLOv8, Python, and the Ultralytics library to tackle the challenge of detecting all five characters simultaneously. I experimented with two distinct approaches to determine the most effective strategy for character identification. The first approach focused on detecting only the heads of the characters, under the assumption that the heads would be less obstructed in the photos despite being smaller in size. The second approach aimed to detect the full characters, which provided a larger target but was often hindered by obstructions and varying image conditions. By comparing these methods, I evaluated whether the advantage of larger size outweighed the difficulties posed by obstructions. Ultimately, the head-only model proved to be more successful, yielding superior results and more accurate detections. This approach balanced the trade-off between size and visibility, demonstrating that, in this case, focusing on less obstructed, though smaller, features led to better overall performance.

![alt text](/img/posts/waldo-evaluation.png "Model Evaluation")

---

### Example Calculation
For an example, I will set value1 to 48 and value2 to 72. In this example I will find the largest number that divides evenly into both numbers.
```ruby
value1 = 48
value2 = 72

largest_divisor_finder(value1, value2)
```

<br/>
### Numbers to Search for Common Divisors
Next I create a set of all the numbers I want to search through in order to find the largest common divisor. The smallest number (other than 1) that could potentially divide into both numbers is 2, so I begin the set at 2. Then I include each whole number from 2 to the smaller of value1 and value2 using the range function. I write smaller+1 as the range function is not inclusive of the ending number.
```ruby
smaller = min(value1, value2)
    
# divisor range to be checked
divisors = set(range(2, smaller+1))

print(divisors)
>>> {2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48}
```

<br/>
### Loop through the Divisors Set
Next I create a while loop to find common divisors. The while loop runs as long as there are numbers to check in the divisors set. In order to make sure this loop doesn't run forever, I will remove numbers from divisors during each pass through the loop.
```ruby
# iterate until list is empty
while divisors:
```

<br/>
### Find and Test the Next Number from the Divisors Set
The first action inside the loop is to remove the lowest number (2) from divisors. I set the variable test_divisor equal to this number (2).
```ruby
test_divisor = divisors.pop()

print(test_divisor)
>>> 2
print(divisors)
>>> {3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42,43,44,45,46,47,48}
```

<br/>
Next I test to see if test_divisor divides evenly into value1 and value2. If so, then I update the answer to be test_advisor.
```ruby
if value1 % test_divisor == 0 and value2 % test_divisor == 0:
    answer = test_divisor

print(answer)
>>> 2
```

If not, then I remove all multiples of the test_divisor from the divisors set. This will shorten the number of times that the while loop executes.
In this example, this first happens when the test_divisor is 5. Any number divisible by 5 is removed from the divisor set.
```ruby
else:
    multiples_to_remove = set(range(test_divisor*2, smaller + 1, test_divisor))
    divisors.difference_update(multiples_to_remove)
print(multiples_to_remove)
>>> {10,15,20,25,30,35,40,45}
print(divisors)
>>> {6,7,8,9,11,12,13,14,16,17,18,19,21,22,23,24,26,27,28,29,31,32,33,34,36,37,38,39,41,42,43,44,46,47,48}
```

<br/>
### Finish the Loop
I continue executing the loop until there are no more numbers to check in the divisors set. At this point, my answer will be the following:
```         
print(answer)
>>> 24
```

<br/>
### Display the Results
Finally I print the findings: the largest integer that divides evenly into both 48 and 72.
``` 
print(f"The largest integer divisor of the whole numbers {value1} and {value2} is {answer}.")
>>> The largest integer divisor of the whole numbers 48 and 72 is 24.
``` 

<br/>
Now I can pass any 2 positive integers to the function and watch the function do the heavy lifting.

As an example I will pass the large numbers: 128,245 and 134,509,830.

```ruby
largest_divisor_finder(value1=128245, value2=134509830)
>>> The largest integer divisor of the whole numbers 128245 and 134509830 is 65.
```

<br/>
In a few short lines of code I created a tool for finding the largest integer divisor of two whole numbers that operates with speed and accuracy.
