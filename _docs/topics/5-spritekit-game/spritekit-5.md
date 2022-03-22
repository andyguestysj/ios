---
title: Sprites
permalink: /docs/spritekit-5/
---

### Sprites

Making a sprite is a little more involved than adding a background image (as you'd expect). We need to be able to access the sprite throughout the Scene to update it, check for collisions, etc. To this we need to create the sprite as a member variable of our scene class. (The image used in the example is in the assets.zip file [assets.zip](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1169361)).  

You would add the code as shown below.  

We use spriteScale to scale the size of the player sprite (and later the obstacles). You can change this figure if the sprites are to small or big on your screen. 

```swift
class GameScene: SKScene {

  // Creates the player sprite using player-motorbike.jpg
  // Note it is a constant as player is a reference to the sprite player will not change but the contents of the sprite will
  let player = SKSpriteNode(image: "player-motorbike.jpg")
  let spriteScale = 0.75

  override func didMove(to view: SKView) {
    player.position.x = 40
    player.position.y = self.frame.size.height/2
    // lift it above the background layer
    player.zPosition = 1
    player.setScale(spriteScale)
    // attach the player sprite to the scene - adds it to the scene and displays it
    addChild(player)
  }
}
```

What we've added here is a member variable to the scene called `player` which holds all the information related to the player sprite. We've changed its x position, ensured it will be displayed above the background layer and will be visible. It won't do anything, it won't move, you can't interact with it, it won't crash. We'll add those features over the next few pages.  


