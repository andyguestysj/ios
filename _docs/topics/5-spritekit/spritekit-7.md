---
title: Obstacles
permalink: /docs/spritekit-7/
---

### Obstacles

We can add obstacles (or bad guys, power ups, etc) to our game in a number of different ways. We can add them as simple background objects and use physics properties to move them automatically and detecting collisions with them. This is a simple, effect approach when we don't need to give them any sophisticated behaviours.  

### Create Obstacle Function

The function below creates a car obstacle off screen (to the right) at a random height (y value). It adds a `physicsBody` to the sprite so that it moves to the left when the build in timer updates.  

```swift
func createObstacle(){
  // create a random number generator that generators integers within a range
  let randomDistribution = GKRandomDistribution(lowestValue: 50, highestValue: Int((self.frame.self.height - 50)))
  let sprite = SKSpriteNode(imageNamed: "car")
  let carX = Int((self.frame.size.width + 100))

  sprite.position = CGPoint(x: carX, y: randomDistribution.nextInt())
  // give the sprite a name so we can identify it (used for collision detection)
  sprite.name = "enemy"
  // set the zPosition so it is above the background layer
  sprite.zPosition = 1
  sprite.setScale(spriteScale)
  addChild(sprite)
  // Give the sprite a physics body.
  // We use this to give it a velocity so that it will automatically move to the left
  // (and we'll use it later to detect collisions)
  sprite.physicsBody = SKPhysicsBody(texture: sprite.texture!, size: sprite.size)
  sprite.physicsBody?.velocity = CGVector(dx: -500, dy: 0)
  sprite.physicsBody?.affectedByGravity = false
  sprite.physicsBody?.linearDamping = 0
}
```

We can add the following line to the `didMove` method to create a timer that will add cars at regular time intervals.  

```swift
class GameScene: SKScene {

    // create gameTimer to hold a timer
    var gameTimer: Timer?
    let newObstacleRepeatTime = 0.2

    override func didMove(to view: SKView) {

        // attach a scheduled timer to gameTimer
        // this will trigger every 0.35 seconds and call createEnemy
        gameTimer = Timer.scheduledTimer(timeInterval: newObstacleRepeatTime, target: self, selector: #selector(createObstacle)), userInfo: nil, repeats: true)
    }
}
```