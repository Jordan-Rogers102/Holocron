> [!note] In Godot, 1 unit is the equivalent of 1 metre.


# What is a 3D Environment?

A 3D environment in game development is a virtual space where players interact, objects exist, and the game's story unfolds. It consists of three-dimensional models, textures, lighting, and physics simulations to create a realistic and immersive world.

## Coordinate Systems in 3D Environments

3D environments are defined using a coordinate system, which is a set of axes that define the position and orientation of objects within the world. The most common coordinate system in game development is the **right-handed coordinate system**, where:

- The **X-axis** points rightward.
- The **Y-axis** points upward.
- The **Z-axis** points toward the viewer.
# Coordinate System

> [!tip]- Godot is built on "Y up", meaning that the Y axis is the vertical. 
> Other game engines, or 3D Modelling software may be different. 

![[3DWorldsCoordinateSystem.png]]




# Left-handed vs Right-handed Coordinate System
**Left-Handed Coordinate System**

- The X-axis points to the right.
- The Y-axis points upward.
- The Z-axis points toward the viewer.

**Right-Handed Coordinate System**

- The X-axis points to the right.
- The Y-axis points upward.
- The Z-axis points away from the viewer.

**Comparison**

The main difference between the left-handed and right-handed coordinate systems is the direction of the Z-axis. In the left-handed system, the Z-axis points toward the viewer, while in the right-handed system, it points away from the viewer.

This difference affects the way that objects are rotated around the Z-axis. In the left-handed system, a positive rotation around the Z-axis will cause an object to rotate clockwise when viewed from the positive Z-axis. In the right-handed system, a positive rotation around the Z-axis will cause an object to rotate counterclockwise when viewed from the positive Z-axis.

**Which Coordinate System is Used in Game Development?**

The right-handed coordinate system is the most commonly used coordinate system in game development. This is because it is consistent with the way that 3D graphics are rendered on most computer systems.

**Example**

Consider a cube that is positioned at the origin of a coordinate system. If we rotate the cube 90 degrees around the Z-axis in the left-handed system, the cube will rotate clockwise. If we rotate the cube 90 degrees around the Z-axis in the right-handed system, the cube will rotate counterclockwise.

**Note:**

Some game engines and 3D modeling software use the left-handed coordinate system. However, it is more common to use the right-handed coordinate system in game development.