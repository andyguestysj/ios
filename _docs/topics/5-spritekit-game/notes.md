```swift
//
//  ContentView.swift
//  Racing
//
//  Created by user208560 on 3/2/22.
//

import SwiftUI
import SpriteKit
import GameplayKit
class GameScene: SKScene, SKPhysicsContactDelegate {

    let player = SKSpriteNode(imageNamed: "player-motorbike.png")
    var gameTimer: Timer?
    var touchingPlayer = false
    let spriteScale = 0.75
    let newObstacleRepeatTime = 0.2

    override func didMove(to view: SKView) {
      // initialise method
        let background = SKSpriteNode(imageNamed: "road.jpg")
        background.zPosition = -1
        background.position = CGPoint(x: self.frame.size.width/2, y: self.frame.size.height/2)
        background.size = CGSize(width: self.frame.size.width, height: self.frame.size.height)
        addChild(background)

        gameTimer = Timer.scheduledTimer(timeInterval: newObstacleRepeatTime, target: self, selector: #selector(createObstacle), userInfo: nil, repeats: true)

       /* if let particles = SKEmitterNode(fileNamed: "Mud") {
          particles.advanceSimulationTime(10)
          particles.position.x = self.frame.size.width
          particles.position.y = self.frame.size.height/2
          particles.particlePositionRange.dy = self.frame.size.height
          addChild(particles)
        }*/

        // position the player
        player.position.x = 40
        player.position.y = self.frame.size.height/2
        // lift it above the background layer
        player.zPosition = 1
        player.setScale(spriteScale)
        // attach the player sprite to the scene - adds it to the scene and displays it
        addChild(player)
        player.physicsBody = SKPhysicsBody(texture: player.texture!, size: player.size)
        // give the physics body a bit mask that can be used to identify the player sprite
        player.physicsBody?.categoryBitMask = 1
        player.physicsBody?.affectedByGravity = false
        // turn on the collision detection and tell the scene to handle collisions
        physicsWorld.contactDelegate = self
    }

    override func update(_ currentTime: TimeInterval) {

    }

    override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {
        // first we check to see if any new touches have been detected
        // if none have been detected we exit the method
        guard let touch = touches.first else { return }
        // next we get the location of the touch
        let location = touch.location(in: self)
        // next we get a list of all nodes (objects attached directly to the scene) at that location
        let tappedNodes = nodes(at: location)
        // now we check if the player sprite is one of the nodes at the location
        if tappedNodes.contains(player) {
            // if the player sprite is at the location then set touchingPlyer to true
            touchingPlayer = true
        }
    }

    override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {

        // first we check if the player sprite is currently being touched, if it isn't we just exit the method
        guard touchingPlayer else { return }
        // next we check to see if any moving touches have been detected
        // if none have been detected we exit the method
        guard let touch = touches.first else { return }
        // now we know the player sprite and the screen are being touched at the same time
        // we get the position of the touch
        let location = touch.location(in: self)
        // then we move the player sprite to that location
        player.position.y = location.y
    }

    override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {
        // we also need to release the player sprite when the touch ends
        touchingPlayer = false
    }

    @objc func createObstacle(){
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
        sprite.physicsBody?.contactTestBitMask = 1
        // give each sprite a bit mask of 0
        sprite.physicsBody?.categoryBitMask = 0
    }

    func didBegin(_ contact: SKPhysicsContact) {
      // There should be two nodes in any collision, we check to make sure we have two nodes and exit the method if we don't
      guard let nodeA = contact.bodyA.node else { return }
      guard let nodeB = contact.bodyB.node else { return }
      // we want the player sprite to react to hitting the other object, so we need to identify which node is the player and pass the other node to a method which will update the player
      if nodeA == player {
        playerHit(nodeB)
      } else {
        playerHit(nodeA)
      }
    }

    func playerHit(_ node: SKNode) {
        // right now we'll simply remove the player sprite, we'll need to passed in node to do something more interesting later
        player.removeFromParent()
        node.removeFromParent()
    }
}

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