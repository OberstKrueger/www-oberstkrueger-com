---
category: health
created: 2017.03.18:1945
title: The Krueger Report - Exercise Routine
type: page
updated: 2017.03.18:1945
---

# Exercise Routine

## Current Schedule

My exercise routine is a rotating routine that I try to do every day. There are two main components to my daily exercise: a strength training exercise, and a cardio workout. The strength training focuses on different parts of the body so that whatever I worked out one day will get a day or two to rest up following that workout.

### Cardio

My cardio workout follows a three day rotation. The first two days I ride an exercise bike, and then on the third day, I jog around the neighborhood. Due to my work schedule, I do this portion of the workout for 24 minutes on workdays, and aim for 48 minutes on my days off. When I am riding the bike, I use this time to catch up on reading the news and any articles that I have saved for later reading. As I jog, I of course do not read, and I make sure that I am not listening to anything too loud or distracting so that I remain aware of my surroundings.

### Planks

My favorite exercise to do is a [plank](https://en.wikipedia.org/wiki/Plank_(exercise)). This exercise is quick and gives a good workout to the [core muscles](https://en.wikipedia.org/wiki/Core_(anatomy)) of the body.

For every day that I do planks, I hold the position twice. The first time is what I consider the full-length time for the day, and the second time is half of that time. My goal is to be able to hold a plank for 128 seconds, so to calculate this, I use the following [Python](https://en.wikipedia.org/wiki/Python_(programming_language)):

	for day in range(1, 32 + 1):
		print("{}. {} seconds, {} seconds".format(day, day * 4, day * 2))

The first day I start at work seconds, and over a 32-day period, I work up to 128 seconds. This leads to the following 32-day plan for planks.

1. 4 seconds, 2 seconds
2. 8 seconds, 4 seconds
3. 12 seconds, 6 seconds
4. 16 seconds, 8 seconds
5. 20 seconds, 10 seconds
6. 24 seconds, 12 seconds
7. 28 seconds, 14 seconds
8. 32 seconds, 16 seconds
9. 36 seconds, 18 seconds
10. 40 seconds, 20 seconds
11. 44 seconds, 22 seconds
12. 48 seconds, 24 seconds
13. 52 seconds, 26 seconds
14. 56 seconds, 28 seconds
15. 60 seconds, 30 seconds
16. 64 seconds, 32 seconds
17. 68 seconds, 34 seconds
18. 72 seconds, 36 seconds
19. 76 seconds, 38 seconds
20. 80 seconds, 40 seconds
21. 84 seconds, 42 seconds
22. 88 seconds, 44 seconds
23. 92 seconds, 46 seconds
24. 96 seconds, 48 seconds
25. 100 seconds, 50 seconds
26. 104 seconds, 52 seconds
27. 108 seconds, 54 seconds
28. 112 seconds, 56 seconds
29. 116 seconds, 58 seconds
30. 120 seconds, 60 seconds
31. 124 seconds, 62 seconds
32. 128 seconds, 64 seconds

### Push-Ups

Push-ups are another one of my favorite exercises, since they're a quick and straightforward way for building upper body strength.

The routine I use for building up how many push-ups I can do is based on the [Hundred Pushups program](http://hundredpushups.com). In the time since I created this schedule, the Hundred Pushups program has changed its numbers slightly, but the general concept is still the same.

For my own routine, I took the values of the last set of reps that they offered and calculated out the difference between reps. The program gives 8 reps of pushups, followed by the goal amount of push-ups for that session. The last pair of reps were a quarter of the goal, so I set those reps as a base rate. Then when calculating the multipliers for all 8 reps, which came out as follows:

1. 1.2
2. 1.2
3. 1.4
4. 1.4
5. 1.2
6. 1.2
7. 1.0 (base rate)
8. 1.0 (base rate)

I then add a 9th rep, which is the goal for the day.

To calculate the exact numbers of these reps, I used the following [Python](https://en.wikipedia.org/wiki/Python_(programming_language)) code:

	multipliers = [1.2, 1.2, 1.4, 1.4, 1.2, 1.2, 1, 1]
	for day in range(1, 64 + 1):
		output = "{}. ".format(day)
		for multiplier in multipliers:
			count = int(int(day / 2) * multiplier)
			output += "{}, ".format(count if count > 0 else 1)
		print("{}{}".format(output, day * 2))

This assumes a final goal of 128 push-ups, with the starting goal being 2, and adding 2 more for each day. This gives a total of 64 days to work up from a rep of 2 push-ups to the goal. For each date, it calculates the base rate(¼ of the goal), and then applies the multipliers to that base rate. Each of these numbers is truncated to the nearest whole number, and always being at least 1. This gives the first 8 numbers. The goal for the day is then appended as the 9th number.

Using this formula, the daily amount of push-ups is this:

1. 1, 1, 1, 1, 1, 1, 1, 1, 2
2. 1, 1, 1, 1, 1, 1, 1, 1, 4
3. 1, 1, 1, 1, 1, 1, 1, 1, 6
4. 2, 2, 2, 2, 2, 2, 2, 2, 8
5. 2, 2, 2, 2, 2, 2, 2, 2, 10
6. 3, 3, 4, 4, 3, 3, 3, 3, 12
7. 3, 3, 4, 4, 3, 3, 3, 3, 14
8. 4, 4, 5, 5, 4, 4, 4, 4, 16
9. 4, 4, 5, 5, 4, 4, 4, 4, 18
10. 6, 6, 7, 7, 6, 6, 5, 5, 20
11. 6, 6, 7, 7, 6, 6, 5, 5, 22
12. 7, 7, 8, 8, 7, 7, 6, 6, 24
13. 7, 7, 8, 8, 7, 7, 6, 6, 26
14. 8, 8, 9, 9, 8, 8, 7, 7, 28
15. 8, 8, 9, 9, 8, 8, 7, 7, 30
16. 9, 9, 11, 11, 9, 9, 8, 8, 32
17. 9, 9, 11, 11, 9, 9, 8, 8, 34
18. 10, 10, 12, 12, 10, 10, 9, 9, 36
19. 10, 10, 12, 12, 10, 10, 9, 9, 38
20. 12, 12, 14, 14, 12, 12, 10, 10, 40
21. 12, 12, 14, 14, 12, 12, 10, 10, 42
22. 13, 13, 15, 15, 13, 13, 11, 11, 44
23. 13, 13, 15, 15, 13, 13, 11, 11, 46
24. 14, 14, 16, 16, 14, 14, 12, 12, 48
25. 14, 14, 16, 16, 14, 14, 12, 12, 50
26. 15, 15, 18, 18, 15, 15, 13, 13, 52
27. 15, 15, 18, 18, 15, 15, 13, 13, 54
28. 16, 16, 19, 19, 16, 16, 14, 14, 56
29. 16, 16, 19, 19, 16, 16, 14, 14, 58
30. 18, 18, 21, 21, 18, 18, 15, 15, 60
31. 18, 18, 21, 21, 18, 18, 15, 15, 62
32. 19, 19, 22, 22, 19, 19, 16, 16, 64
33. 19, 19, 22, 22, 19, 19, 16, 16, 66
34. 20, 20, 23, 23, 20, 20, 17, 17, 68
35. 20, 20, 23, 23, 20, 20, 17, 17, 70
36. 21, 21, 25, 25, 21, 21, 18, 18, 72
37. 21, 21, 25, 25, 21, 21, 18, 18, 74
38. 22, 22, 26, 26, 22, 22, 19, 19, 76
39. 22, 22, 26, 26, 22, 22, 19, 19, 78
40. 24, 24, 28, 28, 24, 24, 20, 20, 80
41. 24, 24, 28, 28, 24, 24, 20, 20, 82
42. 25, 25, 29, 29, 25, 25, 21, 21, 84
43. 25, 25, 29, 29, 25, 25, 21, 21, 86
44. 26, 26, 30, 30, 26, 26, 22, 22, 88
45. 26, 26, 30, 30, 26, 26, 22, 22, 90
46. 27, 27, 32, 32, 27, 27, 23, 23, 92
47. 27, 27, 32, 32, 27, 27, 23, 23, 94
48. 28, 28, 33, 33, 28, 28, 24, 24, 96
49. 28, 28, 33, 33, 28, 28, 24, 24, 98
50. 30, 30, 35, 35, 30, 30, 25, 25, 100
51. 30, 30, 35, 35, 30, 30, 25, 25, 102
52. 31, 31, 36, 36, 31, 31, 26, 26, 104
53. 31, 31, 36, 36, 31, 31, 26, 26, 106
54. 32, 32, 37, 37, 32, 32, 27, 27, 108
55. 32, 32, 37, 37, 32, 32, 27, 27, 110
56. 33, 33, 39, 39, 33, 33, 28, 28, 112
57. 33, 33, 39, 39, 33, 33, 28, 28, 114
58. 34, 34, 40, 40, 34, 34, 29, 29, 116
59. 34, 34, 40, 40, 34, 34, 29, 29, 118
60. 36, 36, 42, 42, 36, 36, 30, 30, 120
61. 36, 36, 42, 42, 36, 36, 30, 30, 122
62. 37, 37, 43, 43, 37, 37, 31, 31, 124
63. 37, 37, 43, 43, 37, 37, 31, 31, 126
64. 38, 38, 44, 44, 38, 38, 32, 32, 128

My current schedule has me doing push-ups 3-4 times a week. Aiming to complete a new set of push-ups every other day leads to this being an 18 week program, although with skipping exercise days or not being able to complete one day's goal means it will take a few more weeks on top of that.
