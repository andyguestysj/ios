---
title: Scoring
permalink: /docs/spritekit-10/
---

### Keeping Score

Lets add a score system to the game. We'll do a simple time based score, you'll get points for staying alive.  

We need a variable to store the score and a label to display the score on the screen.  

We can add a label to the scene as shown below/.

```swift
class GameScene: SKScene, SKPhysicsContactDelegate {

  // creates a SKLabelNode using the given font
  let scoreLabel = SKLabelNode(fontNamed: "AvenirNextCondensed-Bold")


  override func didMove(to view: SKView)
  {

    scoreLabel.zPosition = 2
    scoreLabel.position.y = (self.frame.size.height - 50)
    addChild(scoreLabel)

  }

}
```

Next we add a variable to hold the score and use a feature of Swift that allows us to attach an observer to a variable. In this case we set an observer on `score` that changes the `scoreLabel` text when `score` changes.  

```swift
class GameScene: SKScene, SKPhysicsContactDelegate {

  // creates a SKLabelNode using the given font
  let scoreLabel = SKLabelNode(fontNamed: "AvenirNextCondensed-Bold")
  var score = 0 {
    didSet {
      scoreLabel.text = "SCORE: \(score)"
    }
  }

  override func didMove(to view: SKView)
  {

    scoreLabel.zPosition = 2
    scoreLabel.position.y = (self.frame.size.height - 50)
    addChild(scoreLabel)
    // we "change" score to 0 to force the label to update and display
    score = 0

  }

}
```

Finally we increment the score in the update.  

```swift
override func update(_ currentTime: TimeInterval) {
  if player.parent != nil {
    score += 1
  }
}
```

