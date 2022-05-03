---
title: More Physics 
permalink: /docs/phys-0/
---

### Physics Bodies

[Apple - Getting started with physics bodies](https://developer.apple.com/documentation/spritekit/sknode/getting_started_with_physics_bodies)  
[Apple - SKPhysicsBody](https://developer.apple.com/documentation/spritekit/skphysicsbody)  

Three types of physics bodies:
* *dynamic volume* simulating a physical object with volume and mass that can be affected by forces and collisions
* *static volume* is similar to a dynamic volume, but its velocity is ignored and it is unaffected by forces or collisions.
* *edge* is a static volume-less body. Edges are never moved by the simulation and their mass doesn’t matter. Edges are used to represent negative space within a scene (such as a hollow spot inside another entity) or an uncrossable, invisibly thin boundary. 

SpriteKit provides a few standard shapes—those based on arbitrary paths and those generated from the alpha channel of a texture. The following figure shows the shapes available:  

<centre>        
    <img src="{{ "/assets/img/physics/physbodies.png" | relative_url }}" alt="Physics Bodies" class="img-responsive">
</centre>

The following code shows how to generate the four physics bodies called out above:

```swift
let spaceShipTexture = SKTexture(imageNamed: "spaceShip.png")
   
// Spaceship 1: circular physics body
let circularSpaceShip = SKSpriteNode(texture: spaceShipTexture)
circularSpaceShip.physicsBody = SKPhysicsBody(circleOfRadius: max(circularSpaceShip.size.width / 2,
                                                                  circularSpaceShip.size.height / 2))
   
// Spaceship 2: rectangular physics body
let rectangularSpaceShip = SKSpriteNode(texture: spaceShipTexture)
rectangularSpaceShip.physicsBody = SKPhysicsBody(rectangleOf: CGSize(width: circularSpaceShip.size.width,
                                                                     height: circularSpaceShip.size.height))
   
// Spaceship 3: polygonal physics body
let polygonalSpaceShip = SKSpriteNode(texture: spaceShipTexture)
let path = CGMutablePath()
path.addLines(between: [CGPoint(x: -5, y: 37), CGPoint(x: 5, y: 37), CGPoint(x: 10, y: 20),
                        CGPoint(x: 56, y: -5), CGPoint(x: 37, y: -35), CGPoint(x: 15, y: -30),
                        CGPoint(x: 12, y: -37), CGPoint(x: -12, y: -37), CGPoint(x: -15, y: -30),
                        CGPoint(x: -37, y: -35), CGPoint(x: -56, y: -5), CGPoint(x: -10, y: 20),
                        CGPoint(x: -5, y: 37)])
path.closeSubpath()
polygonalSpaceShip.physicsBody = SKPhysicsBody(polygonFrom: path)
  
// Spaceship 4: physics body using texture’s alpha channel
let texturedSpaceShip = SKSpriteNode(texture: spaceShipTexture)
texturedSpaceShip.physicsBody = SKPhysicsBody(texture: spaceShipTexture,
                                              size: CGSize(width: circularSpaceShip.size.width,
                                                           height: circularSpaceShip.size.height))
```

The shape of a physics body affects performance. A circular physics body offers the best performance and can be significantly faster than other physics bodies. If your simulation contains many physics bodies, circular bodies are the best solution. Rectangular and polygonal shapes improve collision accuracy with reduced speed. Physics bodies created from the alpha channel of a texture offer the best fidelity at the highest performance cost.  

#### Curvy Ground Example

The code below will create a curved ground based on the splinepoints. This ground is not affected by gravity, will not move but will block the movement of other physics bodies.  

```swift
// Create the ground node and physics body
var splinePoints = [CGPoint(x: 0, y: 500),
                    CGPoint(x: 100, y: 50),
                    CGPoint(x: 400, y: 110),
                    CGPoint(x: 640, y: 20)]
let ground = SKShapeNode(splinePoints: &splinePoints,
                         count: splinePoints.count)
ground.lineWidth = 5
ground.physicsBody = SKPhysicsBody(edgeChainFrom: ground.path!)
ground.physicsBody?.restitution = 0.75
ground.physicsBody?.isDynamic = false
     
// Add the two nodes to the scene
scene.addChild(ground)
```

#### SKPhysicsBody Properties

**Defining How Forces Affect a Physics Body** 
* `var affectedByGravity: Bool` A Boolean value that indicates whether this physics body is affected by the physics world’s gravity.
* `var allowsRotation: Bool` A Boolean value that indicates whether the physics body is affected by angular forces and impulses applied to it.
* `var isDynamic: Bool` A Boolean value that indicates whether the physics body is moved by the physics simulation.

**Defining a Physics Body’s Physical Properties**  
Move a physics body, and make it collide with other objects, by setting its physical properties once or changing them dynamically.  
* `var mass: CGFloat` The mass of the body, in kilograms.
* `var density: CGFloat` The density of the object, in kilograms per square meter.
* `var area: CGFloat` The area covered by the body.
* `var friction: CGFloat` The roughness of the surface of the physics body.
* `var restitution: CGFloat` The bounciness of the physics body.
* `var linearDamping: CGFloat` A property that reduces the body’s linear velocity.
* `var angularDamping: CGFloat` A property that reduces the body’s rotational velocity.

Notes  
* `mass` and `density` are interrelated and calculated from each other using the `area`. If you change `mass` then `density` will be recalculated and vice-versa
* `friction` affects how much frictional force is applied when the body is in contact with another

**Applying Forces and Impulses to a Physics Body**  
Making Physics Bodies Move  
* `func applyForce(CGVector)` Applies a force to the center of gravity of a physics body.
* `func applyTorque(CGFloat)` Applies torque to an object.
* `func applyForce(CGVector, at: CGPoint)` Applies a force to a specific point of a physics body.
* `func applyImpulse(CGVector)` Applies an impulse to the center of gravity of a physics body.
* `func applyAngularImpulse(CGFloat)` Applies an impulse that imparts angular momentum to an object.
* `func applyImpulse(CGVector, at: CGPoint)` Applies an impulse to a specific point of a physics body.

A **force** is applied for a length of time based on the amount of simulation time that passes between when you apply the force and when the next frame of the simulation is processed. So, to apply a continuous force to an body, you need to make the appropriate method calls each time a new frame is processed. Forces are usually used for continuous effects.  

An **impulse** makes an instantaneous change to the body’s velocity that is independent of the amount of simulation time that has passed. Impulses are usually used for immediate changes to a body’s velocity.  

### Physics Links

* [Crocodile & Vines](https://www.raywenderlich.com/5347797-how-to-make-a-game-like-cut-the-rope-with-spritekit)
* [Basic Actions & Physics](https://code.tutsplus.com/tutorials/spritekit-actions-and-physics--cms-28961)
* [Apple - Getting started with physics](https://developer.apple.com/documentation/spritekit/sknode/getting_started_with_physics_bodies)
* [Intro to SpriteKit Physics](https://blog.devgenius.io/spritekit-physics-c8849475c21)  
* [Pachinko Physics Game Example](https://iosexample.com/a-simple-game-application-using-spritekit-physics-blend-modes-radians-and-cgfloat/)
* 
