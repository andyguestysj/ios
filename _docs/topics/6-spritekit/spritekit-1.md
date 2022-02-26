---
title: New Game  
permalink: /docs/spritekit-1/
---

### Creating A SpriteKit project in Xcode

1. Start Xcode
2. Select `Create a new Xcode project`
3. Select `Game` and press `Next`
4. Enter a name for your game in `Product Name`
5. Select your Apple Account for `Team`
6. Enter an `Organisation Identifier` - This would be your company name, I'm using YSJ
7. For `Language` select `Swift`
8. For `Game Technology` select `SpriteKit`
9. Ensure `Include iOS Application` is ticked
10. Ensure the other options are **not ticked** - Include watchOS Application, Include tvOS Application, Include macOS Application
11. Click `Next`
12. Select the folder you want to create the project folder in. Ensure `Source Control: Create Git repository on my Mac` is ticked
13. Click `Create`

This should take you in to a new game project in Xcode. It will look something like the image below.  


<centre>        
    <img src="{{ "/assets/img/spritekit/newproj.png" | relative_url }}" alt="A New SpriteKit Project" class="img-responsive">
</centre>

The left hand side of this window is the browser, it defaults to the files in the project.  
The right hand side shows details about the currently selected file.  
The central area shows the content of the file.  

This process has created the SpriteKit equivalent of the `Hello World` program. You can run it by pressing the play button at the top of the left hand-side of the window. It will take a little while to start up and will be a little clunky. The simulator isn't the smoothest running software and using it on a remote desktop makes things worse.  

### SpriteKit Basics

Sprites are animated textured images. SpriteKit works by using, manipulating and interacting with sprites.  

SpriteKit is an extension to the Swift programming language. Swift is an object oriented language, as is SpriteKit.  

