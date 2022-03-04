---
title: Particles  
permalink: /docs/spritekit-4/
---

### Particle Effects

This background is pretty dull and completely static. We can create the illusion that we are moving along it using a particle effect. These particle effects are build in to SpriteKit and quick and eacy to use.  

1. Create a new file, select `SpriteKit Particle Effect`
2. Select the `Snow` template
3. Call the file `Mud.sks`
4. You should see the particle editor on screen. On the right is the attributes inspector. 
5. We need to change the attributes to better suit our requirements
   1. We want the particles to move from right to left so change `Angle Start to 180` and `Angle Range to 0`
   2. We want them to start on the right hand side of the screen so change `Position Range X to 0` and `Position Range Y to 768`
   3. We don't want gravity to affect the particles so change `Acceleration Y to 0`
   4. Change `Lifetime Start to 12` so the particles have time to cross the screen
   5. We want them to move quickly and all at the same speed so change `Speed Start to 800` and `Speed Range to 0`
   6. We want the particles to be bigger. Change the `Scale Start to 2` and the `Scale Range to 0.5`
   7. Change `Emitter Birthrate to 250`, we want to fill the screen
   8. Change the `Alpha Start to 0.2` and the `Alpha Range to 0.2`
   9. Click the white colour circle next to the colour ramp so we can set an appropriate colour
   10. Click the crayon icon at the top right of the pop up screen (see image below) and select the brown crayon.
   11. Return to the particle attributes and set the `Color Blend Range to 0.3` so we get a range of shades
6. Return to the `GameScene` code

**Particle Attributes** 

<centre>        
    <img src="{{ "/assets/img/spritekit/particle1.png" | relative_url }}" alt="Particle Attributes" class="img-responsive">
</centre>

Scroll down to see the colour ramp.  

<centre>        
    <img src="{{ "/assets/img/spritekit/particle2.png" | relative_url }}" alt="Colour Ramp" class="img-responsive">
</centre>

Crayon color selector.  

<centre>        
    <img src="{{ "/assets/img/spritekit/particle3.png" | relative_url }}" alt="Colour Selector" class="img-responsive">
</centre>

### GameScene code

The attributes set above are a good start but if we want to be able to deal with any screen size we need to modify some figures at run time to match the screen size.  

Update your `GameScene` `didMove()` method by adding the lines below immeadiately after `addChild(background)`

```swift
if let particles = SKEmitterNode(fileNamed: "Mud") {
  particles.advanceSimulationTime(10)
  particles.position.x = self.frame.size.width
  particles.position.y = self.frame.size.height/2
  particles.particlePositionRange.dy = self.frame.size.height
  addChild(particles)
}
```

**Note** particle effects are very intensive in the simulator. You may wish to turn it off while working on the game.