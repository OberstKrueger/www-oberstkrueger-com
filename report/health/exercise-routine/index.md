---
category: health
created: 2017.03.18:1945
title: The Krueger Report - Exercise Routine
type: page
updated: 2017.03.18:1945
---

# Exercise Routine

## Current Schedule

My exercise routine follows a strict 7-day schedule. I do not have set days off from exercise, as a typical week for me ends up with 1 or 2 days being skipped due to my work schedule. In the morning, I rotate between push-ups and riding an exercise bike, with the following schedule:

**Monday:** Push-ups\
**Tuesday:** Exercise bike\
**Wednesday:** Push-ups\
**Thursday:** Exercise bike\
**Friday:** Push-ups\
**Saturday:** Exercise bike\
**Sunday:** Exercise bike

In the evening every night, I also have a session of yoga.

A quick note about my selection of numbers in for all of my exercises. I have a strong liking for integrating 2 separate number systems into my routine: [prime numbers](https://en.wikipedia.org/wiki/Prime_number), and [binary numbers](https://en.wikipedia.org/wiki/Binary_number) that are common in computing. For my exercises, all of my chosen numbers come from the second category. The numbers I primariliy use are 16, 24, 32, 64, and 128.

### Push-Ups

Push-ups are one of my favorite exercises, since they're a quick and straightforward way for building upper body strength.

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

To calculate the exact numbers of these reps, I used the following [Swift](https://en.wikipedia.org/wiki/Swift_(programming_language)) code:

	let goal = 128
	let multipliers = [1.2, 1.2, 1.4, 1.4, 1.2, 1.2, 1, 1]

	var day = 2

	while day <= goal {
		var output = ""
		let x = Int(day / 4)
		var base = x < 1 ? 1 : x
		for multiplier in multipliers {
			let y = Int(Double(base) * multiplier)
			output += String(y < 1 ? 1 : y) + ", "
		}
		output += String(day)
		print(output)
		day += 2
	}

This assumes a final goal of 128 push-ups, with the starting push-ups amount being 2, and adding 2 more for each day. This gives a total of 64 days to work up from a rep of 2 push-ups to the goal. For each date, it calculates the base rate(¼ of the goal), and then applies the multipliers to that base rate. Each of these numbers is truncated to the nearest whole number, and always being at least 1. This gives the first 8 numbers. The goal for the day is then appended as the 9th number.

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

My current schedule has me doing push-ups 3 times a week. Assuming none of my skipped days are push-up days, this gives 21.3̅ weeks from start to finish. This is significantly slow than the 6 weeks that Hundred Pushups aims for you to do, but I prefer a longer and more consistent path to reaching the goal.

### Riding The Exercise Bike

My routine for building up strength here is shorter and more straightforward. When I first began biking, I started at 16 minutes, and each day, I add 30 seconds to that until I reached my maximum of 32 minutes. I started with a middling level of resistance on the bike, and have upped it a little bit as I felt necessary.

### Yoga

When I was in college, I practiced yoga numerous times a week. Back then, there was not a plethora of apps designed to guide you through a yoga routine, nor were there tons of high quality videos on YouTube of the same. I developed my own routines based on readings and examples from [Yoga Journal](http://www.yogajournal.com). The routines I created tended to be 30-45 minutes long, and involved holding a smaller amount of poses for longer periods of time.

Since then, I have tried using a few different apps for guided yoga sessions. The classes in [Yoga Studio](http://yogastudioapp.com) were a mainstay of mine for a few years, but I rarely had the motivation to stick with it for long. The classes were not fun, as they are designed around holding poses for shorter periods of time compared to what I was both used to and liked, although I couldn't place my finger on why at the time.

What I did not know then is that there are many types of yoga. Yoga Studio itself creates its classes on a few different styles of yoga, with a bigger focus on [vinyāsa yoga](https://en.wikipedia.org/wiki/Vinyāsa). This style emphasizes the transition between poses, with a more constant moving throughout the entire sequence. [Iyengar yoga](https://en.wikipedia.org/wiki/Iyengar_Yoga) also factors in, with its inclusion of many standing poses

When researching yoga more in-depth, I found that the style of yoga that I preferred was closer to [yin yoga](https://en.wikipedia.org/wiki/Yin_yoga). This style focuses on holding poses for upwards of 5 minutes, something that I regularly did when I first got into yoga. For myself, yoga is just as meditative as it is a workout. Holding poses for longer periods of time helps with that, as it keeps the pace slow.

The classes provided by Yoga Studio do not hold poses for anywhere near this length of time, but the app does provide the ability to create your own classes.  Using this, I created a few classes that are 24-32 minutes in length, with the poses being held for 4 minutes. Yoga Journal's pose directory provides guidance on the poses I use.

[Bikram yoga](https://en.wikipedia.org/wiki/Bikram_Yoga) classes take place in a heated room up to 42°C/108°F. This is warmer than I can make any room that I have available, but I do try to get as close as I can. Typically, this means getting the room up to 29°C/85°F. It's not perfect, but I have found that it does help with holding some of the poses compared to a significantly colder room.

### The Exercising Soundtrack

Many people enjoy the act of working out. Most of the time, I am not one of those people. Working out is tedious, and even while understanding the health benefits you can get only from exercise, I still find it hard to gather the motivation to do it regularly.

My solution to this problem is to have a soundtrack to the work out that makes it more fun. For all 3 forms of exercise, I have a particular audio playlist that I pull from. This helps me get in the mindset for that workout.

When I do my push-up routine, there is time for just a few songs to play. For this, I rotate through a collection of upbeat soundtrack music. The various [Doom](https://en.wikipedia.org/wiki/Doom_(series)) soundtracks are great for this, as well as the battle themes from [Final Fantasy](https://en.wikipedia.org/wiki/Final_Fantasy).

During my bike riding sessions, I listen to soundtrack music that I have not yet listened to. I have a playlist in iTunes that loads up all music with a playcount of 0. From this list, I play any instrumental music, which tends to be game soundtracks. I listen to this, as I spend most of my time readinig while riding the bike. This lets me focus mentally on something that is more stimulating than the act of exercising. Should I run out of unplayed instrumental music, or run out of things to read, I will switch to working through my podcast queue.

Finally, for my yoga routines, I use the soundtrack to [EVE Online](https://en.wikipedia.org/wiki/Eve_Online). Much of the music in EVE is ambient and relaxing, which fits in perfectly with my goals for yoga. Most tracks are 4 minutes, allowing me to get through 6-8 songs per session. [CCP Games](https://en.wikipedia.org/wiki/CCP_Games) has [released the soundtrack for the whole game for free on Soundcloud](https://soundcloud.com/ccpgames/sets/eve-online-in-game-tracks).
