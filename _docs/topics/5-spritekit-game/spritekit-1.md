---
title: New Game  
permalink: /docs/spritekit-1/
---

### Creating A SpriteKit project in Xcode

Apparently the `Game` option in Xcode is out of date so, to create a new game project you should create a Swift/SwiftUI project as described below.  

Xcode does have autocomplete so use it to make entering code easier.  

1. Start Xcode
2. Select `Create a new Xcode project`
3. Select `App` and press `Next`
4. Enter a name for your game in `Product Name`
5. Select your Apple Account for `Team`
6. Enter an `Organisation Identifier` - This would be your company name, I'm using YSJ
7. For `Interface` select `SwiftUI`
8. For `Language` select `Swift`
9. Click `Next`
10. Select the folder you want to create the project folder in. Ensure `Source Control: Create Git repository on my Mac` is ticked
11. Click `Create`

This should take you in to a new game project in Xcode. It will look something like the image below.  

<centre>        
    <img src="{{ "/assets/img/spritekit/newproj.png" | relative_url }}" alt="A New SpriteKit Project" class="img-responsive">
</centre>

The left hand side of this window is the browser, it defaults to the files in the project.  
The right hand side shows details about the currently selected file.  
The central area shows the content of the file on the left and a preview on the right. The preview will start paused.  

### Enabling SpriteKit

To enable SpriteKit for this project 

1. click on the top level of the project in the explorer on the left.  
2. Scroll down the central window till you find `Frameworks, Libraries, and Embedded Content`
3. Click the `+` symbol just below
4. Select `SpriteKit.framework` (it is easier to find if you search for it) and click `Add`
   
The SpriteKit framework libraries have now been added to your project.  

### Project Components (at this point)

**ProjNameApp** simply starts the application by launching `ContentView()`. If you want to run a different class or method, you would need to change it here.  

**ContentView** is the default "body" of your app. Think of it as being like `main()` in a Java app.  

**Assets** is the folder you will store any sprites, images, sounds, music, etc. in. You can simply drag and drop files in to this folder.  

### Setting Up The Game

Open `ContentView` and import SpriteKit by adding `import SpriteKit` after `import SwiftUI`. Next create your Game Scene by adding the code below after the imports

```swift
class GameScene: SKScene {

}
```

Your game may end up with many scenes. Each scene handles the functionality for a screen. It will handle creating the screen, updating it, processing input and any other code you add.  

Change `struct ContentView: View` as follows  

```swift
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

We get the size of the screen and use that to create a scene that fills the screen.  

The `var scene` section sets up the scene to the specified size. The `scene.scaleMode = .fill` ensures the scene will scale properly when resized.  
THe `var body` section simply starts the scene at the specified size.  

#### Adding startup code for the scene

When a scene is created it automatically calls the method `didMove`. Swift is an object-oriented language so we can override this with our own method as shown below.  

```swift
class GameScene: SKScene {

  override func didMove(to view: SKView) {

  }

}
```

Any code placed in `didMove` will be called when GameScene is created. Think of this as an initialisation method.  

#### Adding update code for the scene

You'll want your game to update itself regularly. An SKScene has a built in method called `update` which is automatically, again we can override this as shown below.  

```swift
class GameScene: SKScene {

  override func update(_ currentTime: TimeInterval) {

  }

}
```

#### Detecting Screen Touches

We're working with touch devices so the main inpput type is through touching the screen. Again there are built in methods for this and we can override them as showne below.  

```swift
class GameScene: SKScene {

  override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {

  }

  override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {

  }

  override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {

  }
}
```

This is the basic setup you probably want to do every time you create a new project. Your `GameScene` should look like this.  

```swift
#import SwingUI
#import SpriteKit

class GameScene: SKScene {

  override func didMove(to view: SKView) {
    // initialise method
  }

  override func update(_ currentTime: TimeInterval) {

  }

  override func touchesBegan(_ touches: Set<UITouch>, with event: UIEvent?) {

  }

  override func touchesMoved(_ touches: Set<UITouch>, with event: UIEvent?) {

  }

  override func touchesEnded(_ touches: Set<UITouch>, with event: UIEvent?) {

  }
}
```
