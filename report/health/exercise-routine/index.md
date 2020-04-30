---
category: health
created: 2017-03-18T19:45Z
title: Exercise Routine
type: page
updated: 2017-09-01T05:45Z
---

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

My final push-up goal is to be able to do 128 push-ups, split into 4 groups. Based on the routine from the [Hundred Pushups](http://hundredpushups.com) program, I came up with 4 values that are multiplied against the day that I am currently on to determine what the makeup of those 4 groups are. The multipliers are as follows:

1. 1.0
2. 1.25
3. 1.0
4. 0.75

To calculate the exact numbers of these reps, I used the following [Python](https://en.wikipedia.org/wiki/Python_(programming_language)) code:

	multipliers = [1, 1.25, 1, 0.75]
	for day in range(1, 32 + 1):
		output = "{}. ".format(day)
		for multiplier in multipliers:
			count = int(day * multiplier)
			output += "{}, ".format(count if count > 0 else 1)
		print(output[0:-2])

Using this formula, the daily amount of push-ups is this:

1. 1, 1, 1, 1
2. 2, 2, 2, 1
3. 3, 3, 3, 2
4. 4, 5, 4, 3
5. 5, 6, 5, 3
6. 6, 7, 6, 4
7. 7, 8, 7, 5
8. 8, 10, 8, 6
9. 9, 11, 9, 6
10. 10, 12, 10, 7
11. 11, 13, 11, 8
12. 12, 15, 12, 9
13. 13, 16, 13, 9
14. 14, 17, 14, 10
15. 15, 18, 15, 11
16. 16, 20, 16, 12
17. 17, 21, 17, 12
18. 18, 22, 18, 13
19. 19, 23, 19, 14
20. 20, 25, 20, 15
21. 21, 26, 21, 15
22. 22, 27, 22, 16
23. 23, 28, 23, 17
24. 24, 30, 24, 18
25. 25, 31, 25, 18
26. 26, 32, 26, 19
27. 27, 33, 27, 20
28. 28, 35, 28, 21
29. 29, 36, 29, 21
30. 30, 37, 30, 22
31. 31, 38, 31, 23
32. 32, 40, 32, 24
