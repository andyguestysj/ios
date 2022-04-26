---
title: Contacts & Collisions 
permalink: /docs/coll-0/
---

Now for a more detailed look at using the SpriteKit physics to detect contacts.  

### Contacts vs contacts

SpriteKit supports two kinds of interaction between physics bodies that come into contact or attempt to occupy the same space:  

* A **contact** is used when you need to know that two bodies are touching each other. In most cases, you use contacts when you need to make gameplay changes when a contact occurs.
* A **collision** is used to prevent two objects from interpenetrating each other. When one body strikes another body, SpriteKit automatically computes the results of the collision and applies impulse to the bodies in the collision.

In this example we are using **contacts**. If we were building a physics based game where we wanted to have objects bounce off each other we would use **collision**.  

### Enabling Physics Bodies 

We can give our game objects physics bodies (a SKPhysicsBody) to enable physics for those bodies.  

```swift
self.physicsBody = SKPhysicsBody(rectangleOf: self.size, 
            center: CGPoint(x: 0.0, y: self.size.height/2))
self.physicsBody?.affectedByGravity = false
```

The first line of the code above creates a `SKPhysicsBody` and attaches it to the game object (in this case `self`). The first parameter `rectangleOf: self.size` creates a rectangular physics body the size of `self`. It will create the body so that the rectangle envelopes the texture of self. The second parameter `center` tells the system where to center the rectangular physics body in relation to the self object. (The specific values here depend on the situation, these are taken from the code used in this section).  

The second line of code tells the system not to apply gravity to the physics object. 

`The ? in this line is interesting. It tells the compiler that the property affectedByGravity should exist and to set it to false, but if it doesn't exist (because the physics body failed to be created) then don't worry about it.`

In SpriteKit games we should give a physics body to every object that could be involved in a contact - the player, any enemies, collectibles, walls, the floor, etc.  

### Gloopdrop

We're going to look at contacts using the gloopdrop game. On Moodle there are two versions of Gloopdrop. One (GloopdropBegin) contains a copy of the project as it should be at the beginning of this exercise. The other (GloopdropEnd) contains a copy of the code after we've completed this exercise. Download GloopdropBegin, unzip it, and open in Xcode on the Mac emulator.  

* [GloopdropBegin](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1184736)
* [GloopdropEnd](https://moodle.yorksj.ac.uk/mod/resource/view.php?id=1184737)

#### Adding Physics Bodies

First we need to add physics bodies to everything that could be involved in a contact - the player object, the collectible drops and the foreground (the foreground is the floor).  

To `Player.swift` at the end of the `init()` method add the code below.  

```swift
// Add physics body
self.physicsBody = SKPhysicsBody(rectangleOf: self.size, center: CGPoint(x: 0.0, y: self.size.height/2))
self.physicsBody?.affectedByGravity = false
```

To `Collectible.swift` at the end of the `init()` method add the code below.  

```swift
// Add physics body
self.physicsBody = SKPhysicsBody(rectangleOf: self.size, center: CGPoint(x: 0.0, y: -self.size.height/2))
self.physicsBody?.affectedByGravity = false
```

To `GameScene.swift`, in the `didMove()` method, just before `addChild(foreground)` add the code below.  

```swift
// Add physics body
foreground.physicsBody = SKPhysicsBody(edgeLoopFrom: foreground.frame)
foreground.physicsBody?.affectedByGravity = false
```

Finally, also within `GameScene.swift` change the following lines  

`var level: Int = 8` to `var level: Int = 1`  
`view.showPhysics = false` to `view.showPhysics = true`  

If you now run the game you should see faint boxes around the player and the collectibles. At this point we have added the physics bodies but we are not using them to detect contacts.  

#### Configuring Physics Categories

We need to setup different categories for the physics objects. This will allow us to determine which objects are involved in contacts and handle the contacts correctly.  

In `SpriteKitHelper.swift` , just after the imports, add  

```swift
// SpriteKit Physics Categories
enum PhysicsCategory {
  static let none:        UInt32 = 0
  static let player:      UInt32 = 0b1   // 1
  static let collectible: UInt32 = 0b10  // 2
  static let foreground:  UInt32 = 0b100 // 4
}
```

We've created four categories. `none` will be used to signify objects which will be ignored for contacts. `player`, `collectible` and `foreground` will be used to identify specific types of objects. Not that the values assigned to each category is a power of two (1, 2, 4). This allows us to use bitwise binary logic to identify which objects take part in contacts using bit masks.  

Now we can setup a number of bit masks for each physics object in the game.  

To `Player.swift` at the end of the `init()` method add the four new lines of code below.  

```swift
// Add physics body
self.physicsBody = SKPhysicsBody(rectangleOf: self.size, center: CGPoint(x: 0.0, y: self.size.height/2))
self.physicsBody?.affectedByGravity = false

// Set up physics categories for contacts
self.physicsBody?.categoryBitMask = PhysicsCategory.player          // used to identify the object 
self.physicsBody?.contactTestBitMask = PhysicsCategory.collectible  // used to identify other objects we want to detect contacts with
self.physicsBody?.collisionBitMask = PhysicsCategory.none           // used to identify other objects we want to detect contacts with
```

To `Collectible.swift` at the end of the `init()` method add the four new lines of code below.  

```swift
// Add physics body
self.physicsBody = SKPhysicsBody(rectangleOf: self.size, center: CGPoint(x: 0.0, y: -self.size.height/2))
self.physicsBody?.affectedByGravity = false

// Set up physics categories for contacts
self.physicsBody?.categoryBitMask = PhysicsCategory.collectible
self.physicsBody?.contactTestBitMask = PhysicsCategory.player | PhysicsCategory.foreground
self.physicsBody?.collisionBitMask = PhysicsCategory.none
```

To `GameScene.swift`, in the `didMove()` method, just before `addChild(foreground)` add the four new lines of code below.  

```swift
// Add physics body
foreground.physicsBody = SKPhysicsBody(edgeLoopFrom: foreground.frame)
foreground.physicsBody?.affectedByGravity = false

// Set up physics categories for contacts
foreground.physicsBody?.categoryBitMask = PhysicsCategory.foreground
foreground.physicsBody?.contactTestBitMask = PhysicsCategory.collectible
foreground.physicsBody?.collisionBitMask = PhysicsCategory.none
```

At this point we have added physics bodies to the game objects and told the system what each physics object is and which contacts we are interested in handling. Next we need to handle the processing of the contacts. 

#### Configure the Physics Contact Delegate

We need to modify `GameScene` to handle the contacts. We could modify our `GameScene` directly but it is better to use an extension to keep your code organised.  

Open `GameScene.swift` and add a new extension to handle the contacts. Add the following to the bottom of the file.  

```swift
// MARK: - COLLISION DETECTION

/* ############################################################ */
/*         COLLISION DETECTION METHODS START HERE               */
/* ############################################################ */

extension GameScene: SKPhysicsContactDelegate {
}
```

This extension now declares that the `GameScene` class can act as a delegate fo `SKPhysicsContactDelegate`. We still need to enable this by adding the following line at the top of the `didMove()` method (in `GameScene`).  

```swift
// Set up the physics world contact delegate
physicsWorld.contactDelegate = self
```

#### Detecting Contacts

Inside the SKPhysicsContactDelegate extension add the following method.

```swift
  func didBegin(_ contact: SKPhysicsContact) {
    // Use bitwise OR to store both physics categories in collision
    let collision = contact.bodyA.categoryBitMask | contact.bodyB.categoryBitMask
    
    // Did the [PLAYER] collide with the [COLLECTIBLE]?
    // use bitwise OR to OR the category types together and then compare to the collision variable
    if collision == PhysicsCategory.player | PhysicsCategory.collectible {
      print("player hit collectible")      
    }

    // Or did the [COLLECTIBLE] collide with the [FOREGROUND]?
    if collision == PhysicsCategory.foreground | PhysicsCategory.collectible {
      print("collectible hit foreground")      
    }
  }
```

If you run the code now you should see messages in the output box describing the collisions that occur. 

#### Handling Contacts

Now we can implement code to handle what actually happens when a contact occurs.  

To `Collectible.swift` at the end of the class, add the two methods shown below.    

```swift
// Handle Contacts
func collected() {
  let removeFromParent = SKAction.removeFromParent()
  self.run(removeFromParent)
}

func missed() {
  let removeFromParent = SKAction.removeFromParent()
  self.run(removeFromParent)
}
```

To `GameScene.swift` update the SKPhysicsContactDelegate extension to 

```swift
extension GameScene: SKPhysicsContactDelegate {
  func didBegin(_ contact: SKPhysicsContact) {
    // Check collision bodies
    let collision = contact.bodyA.categoryBitMask | contact.bodyB.categoryBitMask
    
    // Did the [PLAYER] collide with the [COLLECTIBLE]?
    if collision == PhysicsCategory.player | PhysicsCategory.collectible {
      print("player hit collectible")
      
      // Find out which body is attached to the collectible node
      let body = contact.bodyA.categoryBitMask == PhysicsCategory.collectible ?
        contact.bodyA.node :
        contact.bodyB.node

      // Verify the object is a collectible
      if let sprite = body as? Collectible {
        sprite.collected()
      }
    }

    // Or did the [COLLECTIBLE] collide with the [FOREGROUND]?
    if collision == PhysicsCategory.foreground | PhysicsCategory.collectible {
      print("collectible hit foreground")
      
      // Find out which body is attached to the collectible node
      let body = contact.bodyA.categoryBitMask == PhysicsCategory.collectible ?
        contact.bodyA.node :
        contact.bodyB.node

      // Verify the object is a collectible
      if let sprite = body as? Collectible {
        sprite.missed()
      }
    }
  }
}
```

Run the code to see this all in action. You may want to turn the show physics back off again.  