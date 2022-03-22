---
title: Collisions
permalink: /docs/spritekit-8/
---

### Collisions

We need to detect collisions between the player sprite and the car obstacle sprites. We can do this in SpriteKit by using the physics system.  

First we need to enable the collision detection in the scene. To do this we need our scene to inherit from SKPhysicsContactDelegate as well as SKScene. (Java only lets classes inherit from one parent. Swift, like Python, allows for multiple inheritance).  

```swift
class GameScene: SKScene, SKPhysicsContactDelegate {

}
```

Next we have to give the player sprite a physics body.  

```swift
// add the following lines to didMove(), after the player sprite has been created - after the line "addChild(player)"

// give the sprite a physics body
player.physicsBody = SKPhysicsBody(texture: player.texture!, size: player.size)
// give the physics body a bit mask that can be used to identify the player sprite
player.physicsBody?.categoryBitMask = 1
player.physicsBody?.affectedByGravity = false
// turn on the collision detection and tell the scene to handle collisions
physicsWorld.contactDelegate = self
```

We've already give the car obstacles a physics body, we need to give them their own bit mask, one differnt from the player sprite. Here we also enable the collision detection, asking the system to report when a car obstacle collides with a node with a bit mask of 1 (i.e. the player sprite).  

```swift
// add to the end of createEnemy()

// Enable the detection of collisions with objects with a bit mask of 1
sprite.physicsBody?.contactTestBitMask = 1
// give each sprite a bit mask of 0
sprite.physicsBody?.categoryBitMask = 0
```

Now we have the system detecting collisions, we need to check if it is a valid hit between a player sprite and a car obstacle.  

We add the methods below to our scene class.  

```swift
func didBegin(_ contact: SKPhysicsContact) {
  // There should be two nodes in any collision, we check to make sure we have two nodes and exit the method if we don't
  guard let nodeA = contact.bodyA.node else { return }
  guard let nodeB = contact.bodyB.node else { return }

  // we want the player sprite to react to hitting the other object, so we need to identify which node is the player and pass the other node to a method which will update the player
  if nodeA == player {
    playerHit(nodeB)
  } else {
    playerHit(nodeA)
  }
}

func playerHit(_ node: SKNode) {
  // right now we'll simply remove the player sprite, we'll need to passed in node to do something more interesting later
  player.removeFromParent()
}
```
