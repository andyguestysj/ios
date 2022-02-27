---
title: Backgrounds
permalink: /docs/spritekit-3/
---

### Backgrounds

To add a background to the project simply drag and drop the image file in to the `Assets` folder in Xcode.  

To display the background add the following to the `didMove` method of the scene.  

```swift
let background = SKSpriteNode(imageNamed: "filename.extension")
background.zPosition = -1
addChild(background)
```

The `zPosition` indicates the level the image is on, the greater the number the closer it is to the player. We typically use `-1` for the background (or furthest away) layer. Sprites will be given a positive `zPosition` to make them appear on top of the background.  