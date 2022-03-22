---
title: Animated Sprite 
permalink: /docs/sk-6/
---

### Animated Sprite With Texture Atlas 

The code below is already put together in the project [AnimatedSprite](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1177311). This is on Moodle and can be downloaded, unzipped and loaded in Xcode. If you wish to build up the code yourself the resources (sprite, backgroun, foreground) are [here](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1177312).  

This project is not a complete game, it is a demonstration of sprite animation using an atlas.  

### Creating A Texture Atlas

1. Select the Assets folder
2. Right click on the `+` at the bottom of the assets window. 
3. Select `AR and Textures` > `Sprite Atlas` (You may need to scroll down to find `AR and Textures`)
4. Drag and drop the image files you want to be part of the atlas to the atlas folder (inside the assets folder in Xcode)
5. Rename the folder to something appropriate and delete the empty Sprite folder

That's it, but making use of it requires a bit of work. The code below uses a few extra steps to make the code more reusable.  

You will need create most of the files below and fill in the details as shown. Start with the New Game instructions from the SpriteKit Game section.  

### ContentView.swift

```swift
//
//  ContentView.swift
//  AnimatedSprite
//
//  Created by user208560 on 3/22/22.
//

// Nothing different here, we are simply setting the scene size based on the iOS device selected

import SwiftUI
import SpriteKit

struct ContentView: View {
    var scene: SKScene {
        let scene = GameScene(size: UIScreen.main.bounds.size)
        scene.scaleMode = .fill
        return scene
    }
    
    var body: some View {
        SpriteView(scene: scene)
            .frame(width: scene.size.width, height: scene.size.height)
    }
}
```

### SpriteKitHelper.swift

```swift
//
//  SpriteKitHelper.swift
//  AnimatedSprite
//
//  Created by user208560 on 3/22/22.
//
// This file adds a couple of functions to make using atlases a little easier.

import Foundation
import SpriteKit

// extension SKSpriteNode means that the methods are added to SKSpriteNode for this project
extension SKSpriteNode {
    
    // This method loads the textures from the sprite.atlas and returns them as an array of textures
    func loadTextures(atlas: String, prefix: String, StartsAt: Int, StopsAt: Int) -> [SKTexture] {
        var textureArray = [SKTexture]()
        let textureAtlas = SKTextureAtlas(named: atlas)
        for i in StartsAt...StopsAt {
            let textureName = "\(prefix)\(i)"
            let temp = textureAtlas.textureNamed(textureName)
            textureArray.append(temp)
        }
        return textureArray
    }
 
    // This method starts and progresses the animation cycle 
    func startAnimation(textures: [SKTexture], speed: Double, name: String, count: Int, resize: Bool, restore: Bool) {
        
        if (action(forKey: name) == nil) {
            let animation = SKAction.animate(with: textures, timePerFrame: speed, resize: resize, restore: restore)
            
            if count == 0 {
                let repeatAction = SKAction.repeatForever(animation)
                run(repeatAction, withKey: name)
            } else if count == 1 {
                run(animation, withKey: name)
            } else {
                let repeatAction = SKAction.repeat(animation, count: count)
                run(repeatAction, withKey: name)
            }
            
        }
        
    }
    
}
```

### Player.swift

```swift
//
//  Player.swift
//  AnimatedSprite
//
//  Created by user208560 on 3/22/22.
//
// This project uses a player class to hold all the player information and methods rather than keeping them in GameScene like we did in the first game

import Foundation
import SpriteKit
import GameplayKit

enum PlayerAnimationType: String {
    case walk
}


class Player: SKSpriteNode {
    
    // MARK: - PROPERTIES
    
    // Create an array to store the textures/sprites for the sprite walk animation
    private var walkTextures: [SKTexture]?    
    public var playerSpeed: CGFloat = 1.5
    
    // MARK: - INIT
    
    // init() method sets up the basic information for the player object.
    // it loads the textures from the atlas to walkTextures
    init() {
        let texture = SKTexture(imageNamed: "blob-walk_0")
        super.init(texture: texture, color: .clear, size: texture.size())
        self.walkTextures = self.loadTextures(atlas: "blob", prefix: "blob-walk_", StartsAt: 0, StopsAt: 2)
        self.name = "player"
        self.setScale(1.0)
        self.anchorPoint = CGPoint(x: 0.5, y: 0.0)
        
    }
    
    // required to make init() above work
    required init?(coder aDecoder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }
    
    // walk simply triggers the appropriate animation cycle
    func walk() {
        guard let walkTextures = walkTextures else {
            preconditionFailure("Could not find textures")
        }
        startAnimation(textures: walkTextures, speed: 0.25, name: PlayerAnimationType.walk.rawValue, count: 0, resize: true, restore: true)

    }
    
    // moves the sprite, note the comments included.
    func moveToPosition(pos: CGPoint, direction: String, speed: TimeInterval) {
        // we have three images of a walk cycle moving to the right. We don't have images for moving to the left, instead we flip the image to face it to the left
        switch direction {
        case "L" :
            xScale = -abs(xScale)
        default :
            xScale = abs(xScale)
        }
        // we use an SKAction to gradually move the sprite to the clicked position at its current speed
        // note we have constrained the sprites movement so its y position cannot change (see setupConstraints() below)
        let moveAction = SKAction.move(to: pos, duration: speed)
        run(moveAction)
    }
    
    // constrains the sprites movement so it stays on the ground
    func setupConstraints(floor: CGFloat) {
        let range = SKRange(lowerLimit: floor, upperLimit: floor)
        let lockToPlatform = SKConstraint.positionY(range)
        constraints = [ lockToPlatform ]
    }
    
}
```

### GameScene.swift

```swift
//
//  GameScene.swift
//  AnimatedSprite
//
//  Created by user208560 on 3/22/22.
//
// This class is the scene. It manages everything in the scene

import Foundation
import SpriteKit
import GameplayKit


class GameScene: SKScene {

  // create a player object of the Player class  
    let player = Player()

    override func didMove(to view: SKView) {
        // initialise method
        // set up the background image
        let background = SKSpriteNode(imageNamed: "background_1")
        background.anchorPoint = CGPoint(x: 0, y: 0)
        background.position = CGPoint(x: 0, y: 0)
        background.zPosition = -1
        addChild(background)
        
        // set up the foreground image - in this case a floor
        let foreground = SKSpriteNode(imageNamed: "foreground_1")
        foreground.anchorPoint = CGPoint(x: 0, y: 0)
        foreground.position = CGPoint(x: 0, y: 0)
        foreground.zPosition = 0
        addChild(foreground)
        
        // set up the player object
        player.position = CGPoint(x: size.width/2, y: foreground.frame.maxY)
        player.zPosition = 4
        // enforce the constraing it stays on the floor
        player.setupConstraints(floor: foreground.frame.maxY)
        addChild(player)
        // start the animation cycle
        player.walk()
    }

    override func update(_ currentTime: TimeInterval) {

    }

    func touchDown(atPoint pos : CGPoint) {
        // calculate the distance between the player location and the touch location
        let distance = hypot(pos.x - player.position.x, pos.y - player.position.y)
        // calculate the time required to travel the distance at the players speed
        // calculatedSpeed is misnamed here, it is a time really
        let calculatedSpeed = TimeInterval(distance / player.playerSpeed) / 255
        
        if pos.x < player.position.x {
            player.moveToPosition(pos: pos, direction: "L", speed: calculatedSpeed)
        } else {
            player.moveToPosition(pos: pos, direction: "R", speed: calculatedSpeed)
        }
    }
    
  override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
      for t in touches { self.touchDown(atPoint: t.location(in: self)) }
  }

  override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {

  }

  override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {

  }
}
```
