---
layout: post
title: Finding the Largest Divisor with Python
image: "/posts/primes_image.jpeg"
tags: [Python, Primes]
---

# Overview
In this post I'll create a function in Python that can quickly find the largest integer divisor in common between two whole numbers. For example, if I pass the function a value of 100 and 150, then the function would find the largest common divisor to be 50 (100/50 = 2, 150/50 = 3). No larger number can divide evenly into 100 and 150.

<br/>

# Code Explanation
```ruby
def largest_divisor_finder(value1, value2):
    # find which value is smaller
    value1 = 48
    value2 = 72

    if value1 < value2:
        smaller = value1
    else:
        smaller = value2
    
    
    # divisor range to be checked
    divisors = set(range(2, smaller+1))

    # all whole numbers are divisible by at least 1
    answer = 1
    
    # iterate until list is empty
    while divisors:
        test_divisor = divisors.pop()
        if value1 % test_divisor == 0 and value2 % test_divisor == 0:
            answer = test_divisor
        else:
            multiples_to_remove = set(range(test_divisor*2, smaller + 1, test_divisor))
            divisors.difference_update(multiples_to_remove)

    print(f"The largest integer divisor of the whole numbers {value1} and {value2} is {answer}.")
```

---

### Name the Function
First I name the function largest_divisor_finder, and have that function take two arguments: value1 and value2. value1 and value2 are the two whole numbers which the user wishes to find a common divisor for.
```ruby
def largest_divisor_finder(value1, value2):
```

<br/>
### Example Number
For an example, I will set value1 to 48 and value2 to 72. In this example I find the largest number that divides evenly into both numbers
```ruby
value1 = 48
value2 = 72

largest_divisor_finder(value1, value2)
```

<br/>
### Numbers to Search for Common Divisors
Next I create a set of all the numbers I want to search through in order to find the largest common divisor. The smallest number (other than 1) that could potentially divide into both numbers is 2, so I begin the set at 2. Then I include each whole number from 2 to the smaller of value1 and value2 using the range function. I write smaller+1 as the range function is not inclusive of the ending number.
```ruby
if value1 < value2:
    smaller = value1
else:
    smaller = value2
    
    
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
### Find and Store a Prime Number
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
In this example, any number divisible by 2 (the current test_divisor) is removed from the divisor set.
This concludes the first pass through the while loop.
```ruby
else:
    multiples_to_remove = set(range(test_divisor*2, smaller + 1, test_divisor))
    divisors.difference_update(multiples_to_remove)
print(multiples_to_remove)
>>> {4,6,8,10,12,14,16,18,20,22,24,26,28,30,32,34,36,38,40,42,44,46,48}
print(divisors)
>>> {3,5,7,9,11,13,15,17,19,21,23,25,27,29,31,33,35,37,39,41,43,45,47}
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

As an example I will pass a large numbers: 128,245 and 134,509,830.

```ruby
largest_divisor_finder(value1=128245, value2=134509830)
>>> The largest integer divisor of the whole numbers 128245 and 134509830 is 65.
```

<br/>
In a few short lines of code I created a tool for finding prime numbers with surprising speed and perfect accuracy.
