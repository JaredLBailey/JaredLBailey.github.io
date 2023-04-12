---
layout: post
title: Finding Prime Numbers with Python
image: "/posts/primes_image.jpeg"
tags: [Python, Primes]
---

# Overview
Let's create a function in Python that can quickly find all the prime numbers below a given value.  For example, if we pass the function a value of 100, then the function would find all the prime numbers below 100.

<br/>

# Definition
A prime is a number that can only be divided wholly by itself and 1. 
- 7 is a prime number as no other numbers apart from 1 or 7 divide cleanly into it
- 8 is not a prime number as it can be divided by 1, 2, 4, and 8 without remainders


<br/>

# Code Explanation
```ruby
def primes_finder(n):
    
    # number range to be checked
    number_range = set(range(2, n+1))

    # empty list to append discovered primes to
    primes_list = []

    # iterate until list is empty
    while number_range:
        prime = number_range.pop()
        primes_list.append(prime)
        multiples = set(range(prime*2, n+1, prime))
        number_range.difference_update(multiples)
        
    prime_count = len(primes_list)
    largest_prime = max(primes_list)
    
    print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
```

---

### Name the Function
We start by naming our function primes_finder, and have that function take one argument: n. n acts as the upper limit of the numbers we will search through.
```ruby
def primes_finder(n):
```

<br/>
### Example Number
For an example, we will set n to 20. In this example, we are going to find all prime numbers that are smaller than or equal to 20.
```ruby
n = 20
primes_finder(n)
```

<br/>
### Numbers to Search for Primes
Next we create a set of all the numbers we want to search through in order to find the primes. We know that the smallest true prime number is 2, so we begin our set at 2. Then we include each whole number from 2 to n using the range function. We write n+1 as the range function is not inclusive of the ending number.
```ruby
# number range to be checked
number_range = set(range(2, n+1))

print(number_range)
>>> {2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,20}
```

<br/>
### Keep Prime Numbers in a List
We also create a place to store the prime numbers we discover.

```ruby
primes_list = []
```

<br/>
### Loop through the Search List
Next we create a while loop to find our prime numbers. The while loop runs as long as there are numbers to check in the number_range. In order to make sure this loop doesn't run forever, we will remove numbers from the number_range during each pass through the loop.
```ruby
# iterate until list is empty
while number_range:
```

<br/>
### Find and Store a Prime Number
The first action inside the loop is to remove the lowest number (2) from the number range. We set the variable prime equal to this number (2).
```ruby
prime = number_range.pop()

print(prime)
>>> 2
print(number_range)
>>> {3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
```

<br/>
Next we add this number to our list of prime numbers.
```ruby
primes_list.append(prime)

print(primes_list)
>>> [2]
```

<br/>
### Remove Non-Primes from Numbers Being Searched
Since we have our first prime number, we will use this number to find non-primes in our number range. This will shorten the number of times that we run through the while loop.
In this example, any number divisible by 2 is not a prime number. We find these non-prime numbers with the range function. This function finds all whole numbers starting at 4, ending at 20, and counting by 2.
```ruby
 multiples = set(range(prime*2, n+1, prime))
 
 print(multiples)
 >>> {4,6,8,10,12,14,16,18,20}
```

<br/>
Now that we have a set of non-prime numbers, we will use this information to reduce the number_range we are searching through. This concludes our first pass through the while loop.
```
number_range.difference_update(multiples)

print(number_range)
>>> {3,5,7,9,11,13,15,17,19}
```      

<br/>
### Finish the Loop
We continue passing through the loop until there are no more numbers to check in the number_range. At this point, our prime_list will look like the following:
```         
print(prime_list)
>>> [2,3,5,7,11,13,17,19]
```

<br/>
### Display the Results
We then count the prime numbers, and identify the largest one.
```         
prime_count = len(primes_list)
largest_prime = max(primes_list)

print(prime_count)
>>> 8
print(largest_prime)
>>> 19
```

<br/>
Finally we print some interesting findings: the number of primes that were found, and the largest prime in the list.
``` 
print(f"There are {prime_count} prime numbers between 1 and {n}, the largest of which is {largest_prime}")
>>> There are 8 prime numbers between 1 and 20, the largest of which is 19
``` 

<br/>
Now we can pass any positive integer to our function and it will do the rest.

Let's go for something large, say a million...

```ruby
primes_finder(1000000)
>>> There are 78498 prime numbers between 1 and 1000000, the largest of which is 999983
```
<br/>



We're going to end up using a while loop to iterate through our list and check for primes, but before we construct that I always it valuable to code up the logic and iterate manually first.  This means I can check that it is working correctly before I set it off to run through everything on it's own

So, we have our set of numbers (called number_range to check all integers between 2 and 20. Let's extract the first number from that set that we want to check as to whether it's a prime. When we check the value we're going to check if it is a prime...if it is, we're going to add it to our list called primes_list...if it isn't a prime we don't want to keep it

There is a method which will remove an element from a list or set and provide that value to us, and that method is called *pop*

```ruby
print(number_range)
>>> {2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
```
If we use pop, and assign this to the object called **prime** it will *pop* the first element from the set out of **number_range**, and into **prime**

```ruby
prime = number_range.pop()
print(prime)
>>> 2
print(number_range)
>>> {3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}
```

Now, we know that the very first value in our range is going to be a prime...as there is nothing smaller than it so therefore nothing else could possible divide evenly into it.  As we know it's a prime, let's add it to our list of primes...

```ruby
primes_list.append(prime)
print(primes_list)
>>> [2]
```

Now we're going to do a special trick to check our remaining number_range for non-primes. For the prime number we just checked (in this first case it was the number 2) we want to generate all the multiples of that up to our upper range (in our case, 20).

We're going to again use a set rather than a list, because it allows us some special functionality that we'll use soon, which is the magic of this approach.

```ruby
multiples = set(range(prime*2, n+1, prime))
```

Remember that when created a range the syntax is range(start, stop, step). For the starting point - we don't need our number as that has already been added as a prime, so let's start our range of multiples at 2 * our number as that is the first multiple, in our case, our number is 2 so the first multiple will be 4. If the number we were checking was 3 then the first multiple would be 6 - and so on.

For the stopping point of our range - we specify that we want our range to go up to 20, so we use n+1 to specify that we want 20 to be included.

Now, the **step** is key here.  We want multiples of our number, so we want to increment in steps *of our* number so we can put in **prime** here

Lets have a look at our list of multiples...

```ruby
print(multiples)
>>> {4, 6, 8, 10, 12, 14, 16, 18, 20}
```

The next part is the magic I spoke about earlier, we're using the special set functionality **difference_update** which removes any values from our number range that are multiples of the number we just checked. The reason we're doing this is because if a number is a multiple of anything other than 1 or itself then it is **not a prime number** and can remove it from the list to be checked.

Before we apply the **difference_update**, let's look at our two sets.

```ruby
print(number_range)
>>> {3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20}

print(multiples)
>>> {4, 6, 8, 10, 12, 14, 16, 18, 20}
```

**difference_update** works in a way that will update one set to only include the values that are *different* from those in a second set

To use this, we put our initial set and then apply the difference update with our multiples

```ruby
number_range.difference_update(multiples)
print(number_range)
>>> {3, 5, 7, 9, 11, 13, 15, 17, 19}
```

When we look at our number range now, all values that were also present in the multiples set have been removed as we *know* they were not primes

This is amazing!  We've made a massive reduction to the pool of numbers that need to be tested so this is really efficient. It also means the smallest number in our range *is a prime number* as we know nothing smaller than it divides into it...and this means we can run all that logic again from the top!

Whenever you can run sometime over and over again, a while loop is often a good solution.

Here is the code, with a while loop doing the hard work of updated the number list and extracting primes until the list is empty.

Let's run it for any primes below 1000...

```ruby
n = 1000

# number range to be checked
number_range = set(range(2, n+1))

# empty list to append discovered primes to
primes_list = []

# iterate until list is empty
while number_range:
    prime = number_range.pop()
    primes_list.append(prime)
    multiples = set(range(prime*2, n+1, prime))
    number_range.difference_update(multiples)
```


