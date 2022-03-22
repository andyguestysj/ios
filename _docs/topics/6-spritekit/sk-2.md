---
title: SKAction 
permalink: /docs/sk-2/
---

### Overview

* Single class: SKAction 
* As a role of Façade
* Chainable, reusable, readable 
* Looks like scripting language

### Running Actions

* Run action immediately 
* Copy on add, remove on completion 
* Can be repeated N times or forever

### Sequences

```swift
let action1 = SKAction.scaleX(to: 1.0, duration: 1.0)
let action2 = SKAction.fadeAlpha(to: 1.0, duration: 2.0)
let action3 = SKAction.move(to: newPos, duration: 0.5)
let actionSequence = SKAction.sequence([action1, action2, action3])
self.run(actionSequence)
```

<centre>        
    <img src="{{ "/assets/img/sk/seq.png" | relative_url }}" alt="Sequence" class="img-responsive">
</centre>

### Groups

```swift
let action1 = SKAction.scaleX(to: 1.0, duration: 1.0)
let action2 = SKAction.fadeAlpha(to: 1.0, duration: 2.0)
let action3 = SKAction.move(to: newPos, duration: 0.5)
let actionSequence = SKAction.group([action1, action2, action3])
self.run(actionSequence)
```

<centre>        
    <img src="{{ "/assets/img/sk/group.png" | relative_url }}" alt="Group" class="img-responsive">
</centre>

### Sequence With Group

<centre>        
    <img src="{{ "/assets/img/sk/seqgroup.png" | relative_url }}" alt="Sequence with Group" class="img-responsive">
</centre>

### Timing

```swift
let wait = SKAction.wait(forDuration: 1.0)
let sequence = SKAction.sequence([wait, action1])
```

<centre>        
    <img src="{{ "/assets/img/sk/timing.png" | relative_url }}" alt="Delayed Sequence" class="img-responsive">
</centre>

### Speciality

* Animate with textures 
* Animate with a path (CGPath) 
* Fade in/out, remove from parent 
* Short sounds playback

