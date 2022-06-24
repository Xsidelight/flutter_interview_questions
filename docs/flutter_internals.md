# Flutter Internals

## Flutter Engine

![Flutter Architecture](images/flutter-lecture/flutter-architecture2.png)

 - Flutter Framework is driven by the Flutter engine frame rendering
    - The exceptions are:
        - Gesture
        - Platform messages
        - Device messages
        - Future or http responses

    - The Flutter Framework will not apply any visual changes without having requested by the Flutter Engine frame rendering.

    - If you want a visual change to happen, or if you want some code to be executed based on a timer, you need to **tell the Flutter Engine** That something to be rendered. Usually, at next refresh, the Flutter Engine will then request the Flutter Framework to run some code and eventually provide new scene to render.

## RenderView and RenderObject

`RenderObject`s are used to: 
  - define some area of the screen in terms of dimensions, position, geometry but alo in terms of ***"rendering content"***
  - identify zones of the screen potentially impacted by the gestures

The set of all `RenderObject`s form a tree, called `RenderTree` and is itself a special version of a `RenderView`.

`RenderView` represents the total output surface of the RenderTree and is itself a special version of a RenderObject.

![Render Tree](images/flutter-lecture/render_tree.png)


