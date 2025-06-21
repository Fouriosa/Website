# Aqib Khan (B0037224)
Description of code used in element05 for scene 5
## User interface

- Import Babylon.js Core Components
```typescript
import setSceneIndex from "./../index";

import {
    Scene,
    ArcRotateCamera,
    Vector3,
    Camera,
    Engine,
    Sound
  } from "@babylonjs/core";
  import * as GUI from "@babylonjs/gui";
```

- Creates texts used for the GUI
```typescript
  function createText(scene: Scene, theText: string, x: string, y: string, s: string, c: string, advtex) {
    let text = new GUI.TextBlock();
    text.text = theText;
    text.color = c;
    text.fontSize = s;
    text.fontWeight = "bold"; //can add parameter for this if you wish
    text.left = x;
    text.top = y;
    advtex.addControl(text);
    return text;
  }
```
- Creates the rectangle box for the text in GUI
```typescript
  function createRectangle(scene: Scene, w: string, h: string, x: string, y: string, cr: number, c: string, t: number, bg: string, advtext) {
    let rectangle = new GUI.Rectangle();
    rectangle.width = w;
    rectangle.height = h;
    rectangle.left = x;
    rectangle.top = y;
    rectangle.cornerRadius = cr;
    rectangle.color = c;
    rectangle.thickness = t;
    rectangle.background = bg;
    advtext.addControl(rectangle);
    return rectangle;
  }
```
- Creates the rectangle box for the text in GUI
```typescript
  function createSceneButton(scene: Scene, name: string, note: string, index: number, x: string, y: string, advtex) {
    let button = GUI.Button.CreateSimpleButton(name, note);
        button.left = x;
        button.top = y;
        button.width = "80px";
        button.height = "30px";
        button.color = "white";
        button.cornerRadius = 20;
        button.background = "purple";

        button.onPointerUpObservable.add(function() {
            console.log("THE BUTTON HAS BEEN CLICKED");
            setSceneIndex(index -1);
        });
        advtex.addControl(button);
        return button;
 }
```
- Creates the ability to rotate the camera in the scenes
```typescript
 function createArcRotateCamera(scene: Scene) {
  let camAlpha = -Math.PI / 2,
    camBeta = Math.PI / 2.5,
    camDist = 10,
    camTarget = new Vector3(0, 0, 0);
  let camera = new ArcRotateCamera(
    "camera1",
    camAlpha,
    camBeta,
    camDist,
    camTarget,
    scene,
  );
  camera.attachControl(true);
  return camera;
}
```
- Defines the user interface
```typescript   
  export default function menuScene(engine: Engine) {
    interface SceneData {
      scene: Scene;
      advancedTexture: GUI.AdvancedDynamicTexture;
      button1: GUI.Button;
      button2: GUI.Button;
      camera: Camera;
    }
      
    let scene = new Scene(engine);
    let advancedTexture = GUI.AdvancedDynamicTexture.CreateFullscreenUI("myUI", true);
    var button1 = createSceneButton(scene,"but1", "1",1,"-50px", "120px", advancedTexture);
    var button2 = createSceneButton(scene,"but2", "2", 2,"50px", "120px", advancedTexture);
    var camera = createArcRotateCamera(scene);

 
    let that: SceneData = {
      scene,
      advancedTexture,
      button1,
      button2,
      camera
    };
    
    return that;
  } 
```

## First game scene
## Description
This script utilizes the Babylon.js framework to create a simple 3D scene with shapes.

---

- Import Babylon.js Core Components
```typescript
import {
    Scene,
    ArcRotateCamera,
    Vector3,
    HemisphericLight,
    MeshBuilder,
    Mesh,
    Light,
    Camera,
    Engine,
  } from "@babylonjs/core";
```
- Creates a simple cube
```typescript  
  function createBox(scene: Scene) {
    let box = MeshBuilder.CreateBox("box",{size: 1}, scene);
    box.position.y = 3;
    return box;
  }
```

- Creates a light source
```typescript    
  function createLight(scene: Scene) {
    const light = new HemisphericLight("light", new Vector3(0, 1, 0), scene);
    light.intensity = 0.7;
    return light;
  }
```
- Creates a simple spehre
```typescript      
  function createSphere(scene: Scene) {
    let sphere = MeshBuilder.CreateSphere(
      "sphere",
      { diameter: 2, segments: 32 },
      scene,
    );
    sphere.position.y = 1;
    return sphere;
  }
```
- Creates a flat plane for the ground
```typescript    
  function createGround(scene: Scene) {
    let ground = MeshBuilder.CreateGround(
      "ground",
      { width: 6, height: 6 },
      scene,
    );
    return ground;
  }
```
- Creates camera to allow rotation of scene
```typescript    
  function createArcRotateCamera(scene: Scene) {
    let camAlpha = -Math.PI / 2,
      camBeta = Math.PI / 2.5,
      camDist = 10,
      camTarget = new Vector3(0, 0, 0);
    let camera = new ArcRotateCamera(
      "camera1",
      camAlpha,
      camBeta,
      camDist,
      camTarget,
      scene,
    );
    camera.attachControl(true);
    return camera;
  }
```
- Defines game scene 1
```typescript    
  export default function createStartScene(engine: Engine) {
    interface SceneData {
      scene: Scene;
      box?: Mesh;
      light?: Light;
      sphere?: Mesh;
      ground?: Mesh;
      camera?: Camera;
    }
  
    let that: SceneData = { scene: new Scene(engine) };
    // that.scene.debugLayer.show();
  
    that.box = createBox(that.scene);
    that.light = createLight(that.scene);
    that.sphere = createSphere(that.scene);
    that.ground = createGround(that.scene);
    that.camera = createArcRotateCamera(that.scene);
    return that;
  }
```
## Second game scene
## Description
This script utilizes the Babylon.js framework to create a simple 3D scene with shapes.

---

- Import Babylon.js Core Components
```typescript
import {
    Scene,
    ArcRotateCamera,
    Vector3,
    HemisphericLight,
    MeshBuilder,
    Mesh,
    Light,
    Camera,
    Engine,
    StandardMaterial,
    Texture,
    Color3
  } from "@babylonjs/core";
```

- Creates a light source
```typescript    
  function createLight(scene: Scene) {
    const light = new HemisphericLight("light", new Vector3(0, 1, 0), scene);
    light.intensity = 0.7;
    return light;
  }
```
- Creates a cylinder shape
```typescript    
  function createCylinder(scene: Scene) {
    let cylinder = MeshBuilder.CreateCylinder(
      "cylinder",
      { height: 1, diameter: 0.7 },
      scene
    );
    cylinder.position.x = 1;
    cylinder.position.y = 1;
    cylinder.position.z = 1;
  
    var texture = new StandardMaterial("reflective", scene);
    texture.ambientTexture = new Texture("./assets/reflectivity.png", scene);
    texture.diffuseColor = new Color3(1, 1, 1);
    cylinder.material = texture;
    return cylinder;
  }
```

- Creates a simple sphere
```typescript    

  function createSphere(scene: Scene) {
    let sphere = MeshBuilder.CreateSphere(
      "sphere",
      { diameter: 2, segments: 32 },
      scene,
    );
    sphere.position.y = 1;
    return sphere;
  }
```

- Creates a flat plane for the ground
```typescript    
  function createGround(scene: Scene) {
    let ground = MeshBuilder.CreateGround(
      "ground",
      { width: 6, height: 6 },
      scene,
    );
    return ground;
  }
```
- Creates camera to allow rotation of scene
```typescript    
  function createArcRotateCamera(scene: Scene) {
    let camAlpha = -Math.PI / 2,
      camBeta = Math.PI / 2.5,
      camDist = 10,
      camTarget = new Vector3(0, 0, 0);
    let camera = new ArcRotateCamera(
      "camera1",
      camAlpha,
      camBeta,
      camDist,
      camTarget,
      scene,
    );
    camera.attachControl(true);
    return camera;
  }
```
- Defines game scene 2
```typescript    
  export default function createStartScene(engine: Engine) {
    interface SceneData {
      scene: Scene;
      box?: Mesh;
      light?: Light;
      sphere?: Mesh;
      ground?: Mesh;
      camera?: Camera;
    }
  
    let that: SceneData = { scene: new Scene(engine) };
    // that.scene.debugLayer.show();
  
    that.box = createBox(that.scene);
    that.light = createLight(that.scene);
    that.sphere = createSphere(that.scene);
    that.ground = createGround(that.scene);
    that.camera = createArcRotateCamera(that.scene);
    return that;
  }
```