# Code for Palestine 2017 — Gaza
# Year 3 Course: Android Development
Curriculum for the [Code for Palestine](http://www.pgfapps.ps/codeforpalestine/) 2017 summer camp, Gaza branch, Year 3 course.

Students have a background in web development using the Flask web server framework and experience creating web interfaces using HTML, CSS, and JavaScript.

This two-week course is a first exposure to Android development for students.

# Curriculum Overview
See [here](https://docs.google.com/presentation/d/1E2hq97nSFSaDG1SsOIY46O3nBSzaPpFMgRny_pWwCO8/edit?usp=sharing).

Below is a record of material covered.

*Example Android app* demonstrating material covered in the course:
- [Kontax](https://github.com/mog96/kontax)
- [kontax-server](https://github.com/mog96/kontax-server)

# Calendar
|          | S      | M      | T      | W      | Th     | F      | S      |
|----------|--------|--------|--------|--------|--------|--------|--------|
|7/9-7/15  |        |        |        |        |        | [Day 1](#day-1)  | [Day 2](#day-2)  |
|7/16-7/22 | [Day 3](#day-3)  | [Day 4](#day-4)  | [Day 5](#day-5)  | [Day 6](#day-6)  | [Day 7](#day-7)  | [Day 8](#day-8) | |
|7/23-7/29 | [Day 9](#day-9)  | [Day 10](#day-10) | [Day 11](#day-11) | [Day 12](#day-12) | [Day 13](#day-13) |        |      | 

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

*Begin work on final projects*, starting with layout.

### Exercise
Complete the boarding pass app. Use data binding to populate flight information ([Lesson 6](https://github.com/mog96/code-for-palestine-2017_y3-gaza/tree/master/Lessons/Lesson06-Boarding-Pass-App-With-Data-Binding)).

![GIF](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/GIFs/lesson06_boarding-pass-app-with-data-binding.gif)

## Day 8
Set up Parse Server and integrate with Android.

Continue working on layout and button-triggered transitions between screens.

### Exercise
Follow this setup guide: [Integrating Parse Server with Android](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/PARSE_SETUP.md).

## Day 9
Upload all groups' Android Studio projects to GitHub. Review pushing, pulling, merging to ensure that teammates feel comfortable working on their group's Android Studio project in parallel.

Continue working on layout and button-triggered transitions between screens.

## Day 10
Introduce example app: Kontax, a simple contacts app for Android that syncs with "the cloud."
- [Kontax](https://github.com/mog96/kontax)
- [kontax-server](https://github.com/mog96/kontax-server)

Walk students through app-specific features by adding them to Kontax.

### Exercises
Walk through features requested by students:
- [Accessing the camera](https://developer.android.com/training/camera/photobasics.html) and a user's photos
  - Sometimes requires [rotating an image](https://stackoverflow.com/a/14066265/) using the image's [EXIF orientation tag](http://sylvana.net/jpegcrop/exif_orientation.html)
- Requesting a user's location
- Presenting an [alert dialog](https://developer.android.com/guide/topics/ui/dialogs.html)
- Storing data in Parse Server
- Querying an API and deserializing results
  - Google
  - Coursera
  - Udacity
- Integrating with Facebook
  - Login
  - Reading profile
- Adding server-side functionality
  - Generating a PDF document using data stored in the DB
- Adding an app icon

## Day 11
Continue working on [Day 10](#day-10) material.

## Day 12
*Last day to work on final projects.*

Cover remaining app-specific features requested by students.

### Exercises
Walk through renaining features requested by students [Day 10](#day-10):
- Requesting a user's location
- Integrating with Facebook
  - Login
  - Reading profile
- Adding server-side functionality
  - Generating a PDF document using data stored in the DB
- Adding an app icon

## Day 13
Last day of class. Present final projects.

# Sources
Curriculum based on Udacity course #851: [Developing Android Apps](https://classroom.udacity.com/courses/ud851).

Screen GIFs made using [licecap](https://www.cockos.com/licecap/).
