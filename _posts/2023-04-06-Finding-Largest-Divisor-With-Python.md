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
    divisors = set(range(2, smaller + 1))

    # all whole numbers are divisible by at least 1
    answer = 1
    
    # iterate until list is empty
    while divisors:
        test_divisor = divisors.pop()
        if value1 % test_divisor == 0 and value2 % test_divisor == 0:
            answer = test_divisor
        else:
            print(divisors)
            multiples_to_remove = set(range(test_divisor*2, smaller + 1, test_divisor))
            divisors.difference_update(multiples_to_remove)
            print(multiples_to_remove)
            print(divisors)

    print(answer)  
    print(f"The largest integer divisor of the whole numbers {value1} and {value2} is {answer}.")
```

---

### Name the Function
First I name the function primes_finder, and have that function take one argument: n. n acts as the upper limit of the numbers that the function will search through.
```ruby
def primes_finder(n):
```

<br/>
### Example Number
For an example, I will set n to 20. In this example I find all prime numbers that are smaller than or equal to 20.
```ruby
n = 20
primes_finder(n)
```

<br/>
### Numbers to Search for Primes
Next I create a set of all the numbers I want to search through in order to find the primes. The smallest true prime number is 2, so I begin the set at 2. Then I include each whole number from 2 to n using the range function. I write n+1 as the range function is not inclusive of the ending number.
```ruby
# number range to be checked
number_range = set(range(2, n+1))

print(number_range)
>>> {2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20}
```

<br/>
### Keep Prime Numbers in a List
I also create a place to track and store the prime numbers discovered.

```ruby
primes_list = []
```

<br/>
### Loop through the Search List
Next I create a while loop to find prime numbers. The while loop runs as long as there are numbers to check in number_range. In order to make sure this loop doesn't run forever, I will remove numbers from number_range during each pass through the loop.
```ruby
# iterate until list is empty
while number_range:
```

<br/>
### Find and Store a Prime Number
The first action inside the loop is to remove the lowest number (2) from number_range. I set the variable prime equal to this number (2).
```ruby
prime = number_range.pop()

print(prime)
>>> 2
print(number_range)
>>> {3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
```

<br/>
Next I add this number to the list of prime numbers.
```ruby
primes_list.append(prime)

print(primes_list)
>>> [2]
```

<br/>
### Remove Non-Primes from Numbers Being Searched
Since I have the first prime number, I will use this number to find non-primes in number_range. This will shorten the number of times that the while loop executes.
In this example, any number divisible by 2 is not a prime number. I find these non-prime numbers with the range function. This function finds all whole numbers starting at 4 and ending at 20, counting by 2.
```ruby
 multiples = set(range(prime*2, n+1, prime))
 
 print(multiples)
 >>> {4,6,8,10,12,14,16,18,20}
```

<br/>
Now that I have a set of non-prime numbers, I use this information to reduce number_range. This concludes the first pass through the while loop.
```
number_range.difference_update(multiples)

print(number_range)
>>> {3,5,7,9,11,13,15,17,19}
```      

<br/>
### Finish the Loop
I continue executing the loop until there are no more numbers to check in number_range. At this point, my prime_list will look like the following:
```         
print(prime_list)
>>> [2,3,5,7,11,13,17,19]
```

<br/>
### Display the Results
I count the prime numbers, and identify the largest one.
```         
prime_count = len(primes_list)
largest_prime = max(primes_list)

print(prime_count)
>>> 8
print(largest_prime)
>>> 19
```

<br/>
Finally I print some interesting findings: the number of primes that were found, and the largest prime in the list.
``` 
print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
>>> There are 8 prime numbers between 1 and 20, the largest of which is 19
``` 

<br/>
Now I can pass any positive integer to the function and it will do the heavy lifting.

As an example I will pass a large number: one million.

```ruby
primes_finder(1000000)
>>> There are 78498 prime numbers between 1 and 1000000, the largest of which is 999983
```

<br/>
In a few short lines of code I created a tool for finding prime numbers with surprising speed and perfect accuracy.
