---
title: Sprites
permalink: /docs/spritekit-4/
---

### Sprites

Making a sprite is a little more involved than adding a background image (as you'd expect). We need to be able to access the sprite throughout the Scene to update it, check for collisions, etc. To this we need to create the sprite as a member variable of our scene class. (The image used in the example is in the assets.zip file [assets.zip](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1169361)).  

You would add the code as shown below.  

```swift
class GameScene: SKScene {

  // Creates the player sprite using player-motorbike.jpg
  // Note it is a constant as player is a reference to the sprite player will not change but the contents of the sprite will
  let player = SKSpriteNode(image: "player-motorbike.jpg")

  override func didMove(to view: SKView) {

    // position the player
    player.position.x = -400
    // lift it above the background layer
    player.zPosition = 3
    // attach the player sprite to the scene - adds it to the scene and displays it
    addChild(player)

  }


}

```

