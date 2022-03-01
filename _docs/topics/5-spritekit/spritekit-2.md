---
title: Scenes & Nodes
permalink: /docs/spritekit-2/
---

### Scenes & Nodes

SpriteKit uses a Scene Graph node tree to organise elements of games. What does this mean? It means that every element within a screen is define as a node in a tree graph. Each node can be a single element or a group of elements which are themselves grouped in to a smaller tree.  

<centre>        
    <img src="{{ "/assets/img/spritekit/scene-graph.png" | relative_url }}" alt="Example Node Tree for a game level" class="img-responsive">
</centre>

Here we have an example scene. The scene is represented by the image at the top. Attached to the scene is a background image (groud), a sun image, three windmill images and a car. The car itself has two wheel images attached to it.  

In code terms we create a scene (`SKScene` in SpriteKit terminology) and attach the ground, sun, windmill and car nodes as children to the sceen. We then attach the wheels as child nodes to the car node.  

Every visual element in a SpriteKit game is a node that is attached, directly or indirectly, to a scene. Likewise sounds and music are nodes attached to a scene. There are non-visual/audio elements that can be added like physics and collision detection.  