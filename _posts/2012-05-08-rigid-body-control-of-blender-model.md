---
id: 7
timestamp: 1336521613
author: "Matt Keller"
title: "Rigid Body Control of Blender Model in PS Suite?"
excerpt: "In this post we're going to export a model out of Blender and see if we can import it into a PS Vida emulator."
---

I saw [this tutorial](http://gamefromscratch.com/post/2012/04/30/Exporting-from-Blender-to-PS-Suite-Blender-to-Vita-in-under-5-minutes.aspx) on the Blender.org front page and decided I wanted to play around with it. I took a model that I already had and on my first try was only able to get half of the face. This was due to the fact that I had the mirror modifier on and as such it only copied the original half of the face because that was really where all the data was stored. By applying the modifier though I was able to get the full face to rotate around.  
  
The default outcome of the tutorial is a simple die that rotates in the view when the arrow keys are pressed. I wanted to figure out how to make it pan though. Upon inspecting the code for the model viewer we can see that there is a Matrix4 object that is controlling the camera. An inspection of the base code for the Matrix4 object reveals that it is a 4x4 matrix. The function that was being called to change the angle of the camera was:  
 
```
Matrix4 world = Matrix4.RotationXyz(FMath.Radians(cameraAngleX),FMath.Radians(cameraAngleY),0.0f);
```
  
I needed the analogous function that shifted the world matrix instead of rotated it. I found a function named Translation that accepted 3 floats. This did the trick:  
  
```
Matrix4 world = Matrix4.Translation(FMath.Radians(cameraAngleX),FMath.Radians(cameraAngleY),0.0f);
```
  
Although this change alone had the not altogether undesirable effect of resetting the location after a certain distance. This was an artifact of my using the angles as linear coordinates. The original program would reset the angle after 360 degrees which for angular translation would be invisible to the end user. Not so much with rectangular coordinates.  
  
I this seem to be that the way this tutorial is creating this object viewer is akin to the initial way transformations were made it this [OpenGL Tutorial](http://www.videotutorialsrock.com/), where at first it was easier to move the world than the camera.  
  
**In Sum:**  
- Sony seems to be coming around a bit to the Android and Apple way of doing things.  
- Graphics are fun. I should do more.