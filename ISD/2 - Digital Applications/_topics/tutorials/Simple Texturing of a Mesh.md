---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 8
---


> [!info] Texturing is the process of applying an image to a 3D object.

> [!faq]- For more information
> [Texturing and Materials - Game Dev Insider](https://gamedevinsider.com/making-games/game-artist/texturing-and-materials/)

Before you can texture, you need to have completed a mesh. A Mesh is a 3D shape which has a shape, but by default has no texture and appears as a grey object.

For instance, this simple light pole. This is made up of a number of different meshes (CSGBoxes and a CSGCylinder).

It’s basic, however it works for this purpose. However the colour is bland.

![[textureBefore.png]]

> [!info] Simple objects can be modelled in Godot, however to create more complex objects, you would need to use an external 3D modelling piece of software such as Blender. For a quick development process, create simple objects that you can quickly texture.


> [!info] When texturing objects, you can use Google Images to search for appropriate textures. If you’re creating an object that requires a repeating texture (like grass on the ground) it is advisable that you search for `<object> texture seamless`, for instance `grass texture seamless` as the images that it offers will not show any edges when tiled next to each other.

Find the images that you wish to texture your object. Import the image into the Godot project.

Select the mesh that you wish to texture. You may need to texture each segment individually.

![[textureSelectNode.png]]

Expand Geometry in the Inspector, then click the down arrow next to Material and choose New ShaderMaterial.

![[textureNewShader.png]]

Drag the texture file from the file system tab to the Material. 

![[textureApplyTexture.png]]
The mesh should then be textured with the image.

![[textureTexturedMesh.png]]

Continue the process until all the meshes in the scene are textured as desired.

![[commonBlocks#Commit & Push]]