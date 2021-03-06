---
title: Backgrounds
permalink: /docs/spritekit-3/
---

### Backgrounds

To add a background to the project simply drag and drop the image file in to the `Assets` folder in Xcode.  

To display the background add the following to the `didMove` method of the scene.  

```swift
let background = SKSpriteNode(imageNamed: "road.jpg")
background.zPosition = -1
background.position = CGPoint(x: self.frame.size.width/2, y: self.frame.size.height/2)
background.size = CGSize(width: self.frame.size.width, height: self.frame.size.height)
addChild(background)
```

The `zPosition` indicates the level the image is on, the greater the number the closer it is to the player. We typically use `-1` for the background (or furthest away) layer. Sprites will be given a positive `zPosition` to make them appear on top of the background.  

Now we grab the size of the screen from `self.frame.size` and use them to position and size the background.  

If you download the [assets.zip](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1169361) file from moodle you'll find an image called `road@2x.jpg` in it you can use to create a dirt road background. (The @x2 tells SpriteKit to display at x 2 resolution, the standard resolution for iPads). Download the zip file, extract the images and drag them to the `Assets` folder in your Xcode project.   

Add the following to your `GameSceen`  

```swift
class GameScene: SKScene  {
  let background = SKSpriteNode(imageNamed: "road.jpg")
  background.zPosition = -1
  addChild(background)

  override func didMove(to view: SKView) {
    let background = SKSpriteNode(imageNamed: "road.jpg")
    background.zPosition = -1
    background.position = CGPoint(x: self.frame.size.width/2, y: self.frame.size.height/2)
    background.size = CGSize(width: self.frame.size.width, height: self.frame.size.height)
    addChild(background)
  }
}
```


