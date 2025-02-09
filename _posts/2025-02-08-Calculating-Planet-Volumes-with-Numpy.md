---
layout: post
title: Calculating Planet Volumes with Numpy
image: "/posts/01-solar-system-pia12114_orig.avif"
tags: [Numpy]
---

In this post, I'm going to use the numpy array function to calculate the volumes of all the Planets in our solar system based on their radius measurements. Once we've done this, we will crank this up and calculate the volume of  1 million planets, just to show the power and speed that which numpy arrays can undertake calculations.

Let's get into this!

---

First, let's start by ensuring we hvae all the numpy functionaility to carry out this project. To do this we will import the numpy library

```ruby
import numpy as np
```

Let's start by creating a one dimensional array containing the radii of all the 8 planets in our solar system

```ruby
radii = np.array([2439.7,6051.8,603171,3389.7,69911,58232,25362,24622])
```
As you may know, the formula for calculating the volume of a sphere is **V = 4/3 π r³**. An example of how we can caluclate the volume of a planet of radius 10 in python is

```ruby
r = 10
volume = 4/3 *np.pi * r**3
print(volume)
>>> 4188.790204786391
```
This is pretty cool. However, our task isn't to calculate the volume of a single planet. Instead, we want to simultaneously calculate the volume of all 8 planets. To do this we could create a loop that iterates through each planet, or we can use numpy to do the same thing in one swift motion.
Let's copy down these 2 lines of code and paste them below. Thenm let's change **volume** to **volumes** and **r** to  our **radii** object. This will apply our calculation to all our radii in our array at the same time.

```ruby
volumes = 4/3 *np.pi * radii**3
print(volumes)
>>> [6.08272087e+10 9.28415346e+11 9.19199899e+17 1.63144486e+11
 1.43128181e+15 8.27129915e+14 6.83343557e+13 6.25257040e+13]
```
Amazing! We are instantly returned an array of the volumes of all 8 planets in our solar system. This is pretty cool, but let me show you something that is even cooler.
Let's crank this up a step and overwrite our radii object with a 1d array that contains 1 million random integers between 1 and 10000. These values will represent the radius measurements of 1 million fictional plantets.

```ruby
radii=np.random.randint(1,1000,1000000)
```
If we look in our variable explorer we now see our radii object has a size of 1000000. Let's now calculate the volume of each one of these 1 million planets using numpy. How long do you think this might take? It has to run this calculation for 1 million values
Let's copy the same calculation code we used before as we will be using the same logic and see just how long it takes.

```ruby
volumes = 4/3 *np.pi * radii**3
print(volumes)
>>> [6.55926089e+08 3.18787249e+09 2.19130796e+08 ... 1.44910530e+09
 9.09310122e+08 1.18846974e+08]
```

Wow! That took no time at all. Fractions of a second. This just highlights how impressive numpy is with its mathematical calculations.

In summary, we could have done this in other ways, but numpy gives us a really clean and fast method. The reason this approach is so fast is that a single numpy array can only contain a single data type whereas lists or tuples could contain a number of different data types. This restriction means that numpy is able to send the task to the highly optimised C code that numpy is built upon. Ultimately, this results in a huge boost in computational speed compared to a normal python procedure involving a **for** loop in conjuction with a list, where the data type for each item must be checked.For high volumes of data with a large amount of iterations, this takes a lot of time. 

While this may be a short and simple project, it showcases just how amazing  numpy is in it's ability for mathematical processing.

