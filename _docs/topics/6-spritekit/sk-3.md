---
title: Physics Engine 
permalink: /docs/sk-03/
---

### Physics Simulation

<centre>        
    <img src="{{ "/assets/img/sk/physicssim.png" | relative_url }}" alt="Physics Simulation in SpriteKit" class="img-responsive">
</centre>

<centre>        
    <img src="{{ "/assets/img/sk/physbody.png" | relative_url }}" alt="Physics Bodies" class="img-responsive">
</centre>

* Sprite kit manages synchronization details 
* Physic-enabled nodes + no-physic nodes

### SKPhysicsBody

* Multiple types of 
shape: 
  * Circle
  * Rectangle
  * EdgeLoopFromRect
  * Edge
  * Polygon
  * EdgeChain
  * EdgeLoopFromPath
* Directly set to 
SKNode’s property

### SKPhysicsWorld

* Combine with SKScene 
* Has gravity property 
* Manage collision details

### Collisions

* SKPhysicsContactDelegate & SKPhysicsContact used to detect collisions  
* collisionBitMask can be used to create groups




