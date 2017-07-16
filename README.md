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
Introduce Java. Begin Android development.

### Objective
Scrolling weather app that fetches data from an API, and displays it in a scrollable TextView.

![GIF](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/GIFs/lesson02_weather-app-with-scrollview.gif)

## Day 3
Cover **Git** usage, before having students pull Day 3 exercise files.
- Clone
- Check out branch
- Commit
- Pull
Leave 'Push' for when we start projects.

### Objective
Finish yesterday's objective.

## Day 4
Learn about Intents and multiple activities in an Android app.

### Objective
Add forecast detail activity to the weather app, shown when a user taps a forecast in the main activity.

Add sharing of forecast text from detail activity.

Add opening map from main activity. (Future version of the weather app will support weather map...?)

![GIF](https://github.com/mog96/code-for-palestine-2017_y3-gaza/blob/master/GIFs/lesson03_weather-app-with-detail-map-share.gif)

## Day 5
Learn about the RecyclerView.
- RecyclerView allows us to scroll through views in list form
- RecyclerView goes hand in hand with an Adapter
- Adapter manages the list of views being scrolled by wrapping each view in an AdapterViewHolder
- AdapterViewHolder is a wrapper around a view in the list
- AdapterViewHolder controls the layout components inside the view, and handles things like clicks on the view

### Objective
Replace ScrollView and TextView with RecyclerView and ViewHolders for each forecast item. (47 TODO items)

# Sources
Curriculum based on Udacity course #851: [Developing Android Apps](https://classroom.udacity.com/courses/ud851).

Screen GIFs made using [licecap](https://www.cockos.com/licecap/).
