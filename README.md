# arcore_flutter_plus 🚀

An enhanced and updated version of the ARCore Flutter plugin. This package allows you to experience Augmented Reality (AR) on Android devices using Google ARCore.

---

### 🙏 Credits & Origin
This package is a **maintained fork** of the original [arcore_flutter_plugin](https://pub.dev/packages/arcore_flutter_plugin) created by **Marco Gomiero**. 
Since the original package has been inactive for several years, **arcore_flutter_plus** aims to keep the plugin alive by providing:
* Compatibility with modern Flutter 3.x versions.
* Support for updated Android SDKs.
* New custom features and bug fixes.

---

## ✨ Key Enhancements (What's New?)

In addition to all the original features, this version includes:

* **Fixed Model Loading:** Give support for `.glb` and `.sfb` 3d models.
* **Custom Shapes:** Added support for new shapes like.
* **Improved Documentation:** Clearer examples for distance measurement and interactive model placement.

---

## 🚀 Getting Started

### 1. Requirements
* **Android API Level:** 24 (Android 7.0) or higher.

### 2. Installation
Add this to your `pubspec.yaml`:
```yaml
dependencies:
  arcore_flutter_plus: ^1.0.0

### 3. Add Permisions
Ensure your AndroidManifest.xml includes ARCore permissions:

XML
<uses-permission android:name="android.permission.CAMERA" />
<uses-feature android:name="android.hardware.camera.ar" />

## 4. Adding assets and models
Add your .glb models to android/app/src/main/assets/.

📖 Usage Example: Placing a Model
Dart
ArCoreReferenceNode node = ArCoreReferenceNode(
  name: "Tom",
  object3DFileName: "tom.glb",
  position: vector.Vector3(0, 0, -1.0),
);
arCoreController.addArCoreNode(node);

## Example

The simplest code example:

```dart
import 'package:arcore_flutter_plugin/arcore_flutter_plugin.dart';
import 'package:flutter/material.dart';
import 'package:vector_math/vector_math_64.dart' as vector;

class HelloWorld extends StatefulWidget {
  @override
  _HelloWorldState createState() => _HelloWorldState();
}

class _HelloWorldState extends State<HelloWorld> {
  ArCoreController arCoreController;

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: const Text('Hello World'),
        ),
        body: ArCoreView(
          onArCoreViewCreated: _onArCoreViewCreated,
        ),
      ),
    );
  }

  void _onArCoreViewCreated(ArCoreController controller) {
    arCoreController = controller;

    _addSphere(arCoreController);
    _addCylindre(arCoreController);
    _addCube(arCoreController);
  }

  void _addSphere(ArCoreController controller) {
    final material = ArCoreMaterial(
        color: Color.fromARGB(120, 66, 134, 244));
    final sphere = ArCoreSphere(
      materials: [material],
      radius: 0.1,
    );
    final node = ArCoreNode(
      shape: sphere,
      position: vector.Vector3(0, 0, -1.5),
    );
    controller.addArCoreNode(node);
  }

  void _addCylindre(ArCoreController controller) {
    final material = ArCoreMaterial(
      color: Colors.red,
      reflectance: 1.0,
    );
    final cylindre = ArCoreCylinder(
      materials: [material],
      radius: 0.5,
      height: 0.3,
    );
    final node = ArCoreNode(
      shape: cylindre,
      position: vector.Vector3(0.0, -0.5, -2.0),
    );
    controller.addArCoreNode(node);
  }

  void _addCube(ArCoreController controller) {
    final material = ArCoreMaterial(
      color: Color.fromARGB(120, 66, 134, 244),
      metallic: 1.0,
    );
    final cube = ArCoreCube(
      materials: [material],
      size: vector.Vector3(0.5, 0.5, 0.5),
    );
    final node = ArCoreNode(
      shape: cube,
      position: vector.Vector3(-0.5, 0.5, -3.5),
    );
    controller.addArCoreNode(node);
  }

  @override
  void dispose() {
    arCoreController.dispose();
    super.dispose();
  }
}


## Documentation 

### Classes provided by the plugin

**There are a total of 13 classes provided by this plugin until Feb 20206.**

- ArCoreView
- ArCoreController
- ArCoreFaceView
- ArCoreFaceContrller
- ArCoreSphere
- ArCoreCylinder
- ArCoreCube
- ArCoreNode
- ArCoeMaterial
- ArCoreHitTestResult
- ArCoreRotatingNode
- ArCorePlane
- ArCoreReferenceNode

---

### ArCoreView

This class returns the view type. There are two types of views in it.

**AUGMENTEDFACE**
**STANDARDVIEW**

There are 4 properties in it:
- onArCoreViewCreated
- enableTapRecoginzer
- enableUpdateListener
- type

---

### onArCoreViewCreated

This property takes a **ArCoreController**.

---

**enableTapRecoginzer**

Initially, set to false. It is used as an argument by the MethodChannel.

---

**enableUpdateListener** 

Initially, set to false. It is used as an argument by the MethodChannel.

---

**type**

It is a view type, it is either **AUGMENTEDFACE, STANDARDVIEW***. It is set to **STANDARDVIEW** by default.

---
### ArCoreController

This controller used to add a ArNode using addArCoreNode function, add a ArCoreNode with ancher using a addArCoreNodeWithAncher function and also remove node using removeNode function.

---

### ArCoreFaceView
It is a stateful widget that returns a **ArCoreAndroidView**. It has two properties **enableAugmentedFaces, onArCoreViewCreated**.

Initially, **enableAugmentedFaces** is set to false.
**onArCoreViewCreated** takes a function with **ArCoreController** argument.

---

### ArCoreFaceController
It used dispose and **loadMesh** method to control the **FaceView**.

---

### ArCoreSphere
It is **ArCoreShape**, takes a **radius & ArCoreMaterial**.

---

### ArCoreCylender
It is **ArCoreShape**, takes a **radius, height, & ArCoreMaterial**.

---

### ArCoreCube
It is **ArCoreShape**, takes a size i.e. **Vector3 & ArCoreMaterial**.

---

### ArCoreNode
This widget is used to provide the **position, shape, scale, rotation, name**.

---

### ArCoreMaterial
It is used to describe the outlook of the virtual object created by the user.

It has **color,textureBytes, metallic, roughness, reflection**.

---

### ArCoreRotatingNode
It is an **ArCoreNode** with a **degreesPerSecond** *property* which is a double value.

---

### ArCorePlane
It takes the **x, y** coordinate of the plane, **ArCorePose & ArCorePlaneType**.

There are three types of plane:
- **HORIZONTAL_UPWARD_FACING**
- **HORIZONTAL_DOWNWARD_FACING**
- **VERTICAL**

---

### ArCoreReferenceNode
It is ArCoreNode, it has all the properties that the ArCoreNode has also it has objectUrl and object3DFileName.

---

### objectUrl
URL of glft object for remote rendering.

---

### object3DFileName
Filename of sfb object in assets folder.
