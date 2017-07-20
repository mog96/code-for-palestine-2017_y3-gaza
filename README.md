# Curriculum Overview
See [here](https://docs.google.com/presentation/d/1E2hq97nSFSaDG1SsOIY46O3nBSzaPpFMgRny_pWwCO8/edit?usp=sharing).

# Calendar
|          | S      | M      | T      | W      | Th     | F      | S      |
|----------|--------|--------|--------|--------|--------|--------|--------|
|7/9-7/15  |        |        |        |        |        | Day 1  | Day 2  |
|7/16-7/22 | Day 3  | Day 4  | Day 5  | Day 6  | Day 7  | Day 8  | Day 9  |
|7/23-7/29 | Day 10 | Day 11 | Day 12 | Day 13 |        |        |        |

## Day 1
Introduce technology stack:
  - Parse Server back end
  - Android front end

Install Android Studio. (Could take a lifetime on the connection here.)

## Day 2
Introduce Java. Begin Android development ([Lesson 1](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson01-ScrollView-Demo)).

### Exercise
Build a weather app that fetches data from an API, and displays it in a scrollable TextView ([Lesson 2](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson02-Weather-App-Using-ScrollView)).

![GIF](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/GIFs/lesson02_weather-app-with-scrollview.gif)

## Day 3
Cover **Git** usage, before having students pull Day 3 exercise files.
- Clone
- Check out branch
- Commit
- Pull
Leave 'Push' for when we start projects.

### Exercise
Finish yesterday's exercise ([Lesson 2](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson02-Weather-App-Using-ScrollView)).

## Day 4
Learn about Intents and multiple activities in an Android app.

Learn about the RecyclerView ([Lesson 4](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson04-Weather-App-Using-RecyclerView), for demonstration only).
- RecyclerView allows us to scroll through views in list form
- RecyclerView goes hand in hand with an Adapter
- Adapter manages the list of views being scrolled by wrapping each view in an AdapterViewHolder
- AdapterViewHolder is a wrapper around a view in the list
- AdapterViewHolder controls the layout components inside the view, and handles things like clicks on the view

### Exercise
Add forecast detail activity to the weather app, shown when a user taps a forecast in the main activity ([Lesson 3](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson03-Weather-App-With-Detail-Activity)).

Add ability to share forecast text from detail activity.

Add ability to open map from main activity. (Future version of the weather app will support weather map...?)

![GIF](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/GIFs/lesson03_weather-app-with-detail-map-share.gif)

## Day 5
Introduction to Android UI elements.

Introduction to Android layouts: [video](https://youtu.be/8agCiQzDZys?t=1m18s).

### Exercises
#### Morning Session (3.5 hrs)
Start a new project and try adding different UI elements to a layout. Experiment with tweaking UI of previous exercises.

Start a new project and add a new activity from scratch. Add the ability to take text entered in an EditText in the main Activity and pass it via an Intent to a child Activity to be displayed.

#### Afternoon Session (1.5 hrs)
Start boarding pass app, a.k.a. LayoutMania ([Lesson 5](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson05-Boarding-Pass-App-With-ConstraintLayout)).

![GIF](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/GIFs/lesson05_boarding-pass-app-with-constraintlayout.gif)

## Day 6
Master the ConstraintLayout.

### Exercise
Finish layout of boarding pass app ([Lesson 5](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson05-Boarding-Pass-App-With-ConstraintLayout)).

## Day 7
Learn to use data binding to populate views with data.

Begin work on students' final projects, starting with layout.

### Exercises
Complete the boarding pass app. Use data binding to populate flight information ([Lesson 6](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson06-Boarding-Pass-App-With-Data-Binding)).

![GIF](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/GIFs/lesson06_boarding-pass-app-with-data-binding.gif)

# Sources
Curriculum based on Udacity course #851: [Developing Android Apps](https://classroom.udacity.com/courses/ud851).

Screen GIFs made using [licecap](https://www.cockos.com/licecap/).
