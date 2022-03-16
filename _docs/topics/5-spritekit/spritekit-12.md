---
title: Restarting The Game
permalink: /docs/spritekit-12/
---

### A Better Ending / Restarting

Currently the game simply stops after the player collides with a car. Lets add some code so that the game will restart after a few seconds.  

1. iOS lets you schedule work after a delay by using the DispatchQueue.main.asyncAfter() method. You tell it what time the code should run after and it will do te rest.
2. The time is specified as an absolute time, so to say "two seconds from now" we need to write `.now() +2`. 
3. When that time is reached we need to make the new game scene out of the GameScene. 
4. Once we have the game scene we need to tell it to use aspectFill
5. Finally we need to call `presentScene()` on our scene's view property to make the new scene display


Update `playerHit` as shown below.

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

  DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
    let newScene = GameScene(size: self.size)
    newScene.scaleMode = self.scaleMode
    let animation = SKTransition.fade(withDuration: 2.0)
    self.view?.presentScene(newScene, transition: animation)
  }
}
```

