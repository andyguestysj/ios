---
title: Finishing Touch
permalink: /docs/spritekit-13/
---

### How many cars?

We are constantly creating cars and filling up the memory. We could do with deleting the cars when they are off screen. This is easy to do.  

Update `update` as shown below.  

```swift
override func update(_ currentTime: TimeInterval) {

  for node in children {
    if node.position.x < -200 {
      // the cars are the only nodes that should get to this position.
      node.removeFromParent()
    }
  }

  // rest of the code
}
```