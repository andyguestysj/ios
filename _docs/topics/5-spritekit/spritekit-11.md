---
title: A Better Ending
permalink: /docs/spritekit-11/
---

### A Better Ending

Currently when we collide with a car the car and you both disappear and the score stops increasing. Lets see if we can do something a bit more interesting.  

#### Game Over

Download ["gameOver-1@2x.png"](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1175064) from moodle and add it to your assets folder in Xcode.  

Update the `playerHit` function as follows

```swift
func playerHit(_ node: SKNode) {
  player.removeFromParent()

  let gameOver = SKSpriteNode(imageNamed: "gameOver-1")
  gameOver.zPosition = 10
  gameOver.position = CGPoint(x: self.frame.size.width/2, y: self.frame.size.height/2)
  addChild(gameOver)
}
```

#### Explosion

Lets use another particle effect.  

Create a new particle effect (File, New File, Particle). Make it a `Fire` effect and name it `Explosion`.

Change the particle effect values as follows:

* Angle Range 360
* Emitter Maximum 200


Update the `playerHit` function as follows

```swift
func playerHit(_ node: SKNode) {

  if let particles = SKEmitterNode(fileNamed: "Explosion.sks") {
    particles.position = player.position
    particles.zPosition = 3
    addChild(particles)
  }


  player.removeFromParent()

  let gameOver = SKSpriteNode(imageNamed: "gameOver-1")
  gameOver.zPosition = 10
  gameOver.position = CGPoint(x: self.frame.size.width/2, y: self.frame.size.height/2)
  addChild(gameOver)
}
```




