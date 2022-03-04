---
title: Touchscreen
permalink: /docs/spritekit-6/
---

### Touchscreen Interaction

We've already added three methods to enable touchscreen interaction.  

```swift
class GameScene: SKScene {

  override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {

  }

  override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {

  }

  override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {

  }
}
```

It won't surprise you to discover that `touchesBegan` gets called when they player touches the screen, `touchesMoved` gets called when a touch point moves, and `touchesEnded` gets called when the touch is removed. Since iPads are multi-touch devices, we will have to examine a list of touches to see what has happened.  

We'll start with the following code.  

```swift
class GameScene: SKScene {

  // Create a boolean flag to indicate if the player is touching the player sprite
  var touchingPlayer = false  

  override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
      // first we check to see if any new touches have been detected
      // if none have been detected we exit the method
      guard let touch = touches.first else { return }

      // next we get the location of the touch
      let location = touch.location(in: self)

      // next we get a list of all nodes (objects attached directly to the scene) at that location
      let tappedNodes = nodes(at: location)

      // now we check if the player sprite is one of the nodes at the location
      if tappedNodes.contains(player) {
          // if the player sprite is at the location then set touchingPlyer to true
          touchingPlayer = true
      }

  }
}
```

The code in `touchesBegan` first checks to see if there have been any touches, then uses the location of the touch to identify any nodes that are directly attached to the scene at that location and then checks to see if any of those nodes is the player node.  

It doesn't actually mode the player sprite though. To do that we can add some code to `touchesMoved`.  

```swift
class GameScene: SKScene {

  override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {
      // first we check if the player sprite is currently being touched, if it isn't we just exit the method
      guard touchingPlayer else { return }

      // next we check to see if any moving touches have been detected
      // if none have been detected we exit the method
      guard let touch = touches.first else { return }

      // now we know the player sprite and the screen are being touched at the same time
      // we get the position of the touch
      let location = touch.location(in: self)
      // then we move the player sprite to that location
      player.position.y = location.y
  }

  override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {
      // we also need to release the player sprite when the touch ends
      touchingPlayer = false
  }
}
```
