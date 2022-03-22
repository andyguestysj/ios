---
title: SKNode 
permalink: /docs/sk-1/
---

### SKNode Hierarchy

<centre>        
    <img src="{{ "/assets/img/sk/sknodesh.png" | relative_url }}" alt="SKNode Hierarchy" class="img-responsive">
</centre>

### SKNode

* Parent class of all nodes.
* Does not display anything
* Stores basic properties
  * position
  * width & height
  * alpha
  * is hidden
  * x & y scaling

### SKSpriteNode

* Display sprites on the screen 
* Has explicit size 
* Can display colors, texture
* Texture atlas support (for animation)
* Can use `colorBlendFactor` to recolour the sprite

<centre>        
    <img src="{{ "/assets/img/sk/colblend.png" | relative_url }}" alt="colorBlebndFactor" class="img-responsive">
</centre>

### SKLabelNode

* Single-line text as a SKNode 
* System fonts 
* Animatable

### SKEmitterNode

* Use for particle system 
* Advanced keyframe sequence controls 
* Built-in particle editor

### SKVideoNode

* Place anywhere, e.g. background 
* Physics enabled

### SKShapeNode

* Dynamic shapes with CGPath 
* Rendered in hardware 
* Stroke/fill

### SKEffectNode

* Group opacity & group blend 
* Can be cached 
* Wrap with a CIFilter

### SKCropNode

* Use to mask a node (any SKNode) 
* SKCropNode can have children, can run 
SKActions