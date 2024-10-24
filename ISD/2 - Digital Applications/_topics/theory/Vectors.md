> [!note]- Tutorial Overview
> This section of the tutorial covers the theory of objects relate to each other in Unity. In this section, you will cover topics such as :
> - Positions
> - Vectors
> - Vector arithmetic
> - Magnitude
> - Dot products
> - Cross products

# Recap: Positions

As you may recall, every object in Godot has a position in the three dimensional space. This position is made up of **three** components - the `x`, `y` and `z` values.

Each object has a world position which is it's position relating to `world zero` (0,0,0).

Notice how these position values are stored in the Transform component of the Game Object. This Transform component is used to store and manipulate the position, rotation and scale of the object it is attached to.

The position, rotation and scale values in a Transform as measured against the Transform's parent. If the Transform has no parent, they are measured against world space.

![vectorsPositionRelative](vectorsPositionRelative.png)

## Relative Positions

As well as having a "world position", each object also has a position in relation to another object. For instance, if an object is a child of another (it appears "underneath" it in the hierarchy) then the child's x, y, and z values are the position (and rotation and scale) in relation to the parent, not world space.

For example, in the picture below, the Capsule's position is 0,0,0 however this is not world zero, but it refers to the centre of the "First Person Controller" object.

Remember: World zero is position 0, 0, 0

![vectorsPositionParent](vectorsPositionParent.png)

# Vectors

![https://www.youtube.com/watch?v=7DK8aA2qee8&ab_channel=Unity](https://www.youtube.com/watch?v=7DK8aA2qee8&ab_channel=Unity)

Vectors in Godo can be viewed as a line between two points (positions) in a 3D space.

In the example below, the red line represents the magnitude between the two positions (the end points of the line).
vector

![vectorsXYZ](vectorsXYZ.jpg)

## Magnitude

> [!tip] The magnitude is simple the length of the vector between two points.

Unity does the calculation for you automatically, however the logic is that knowing the relative position of the two objects, you can use Pythagorus' theorem to calculate the magnitude as can be seen in the image below.

Although this is using a 2d image (Vector2), the logic is the same for a 3d world (Vector3). Instead of **x****2** **+ y****2** **= m****2**, it would be **x****2** **+ y****2** **+ z****2****= m****2**

![vectorsMagnitudeMaths](vectorsMagnitudeMaths.jpg)

## Vector Addition

Vector arithmetic is simply a slightly more complex version of standard addition.

Let's say you have two vectors. The first is (3,5) and the second is (2, -1). When you add these together, you add the first two values, and the second two values - 3+2 and 5+ -1 to give you a final vector of (5, 4).

The process is the same for a 3d vector, just with 3 values. E.g. (2, 1, 2) + (3, 0, 4) = (5, 1, 6).

This can be useful as you can calculate the final position of a game object given two vectors. As can be seen in the video below, give a starting point of 0,0 and with the first movement (first vector) the object moves to 3,5. Then the object makes another move (second vector), and the object reaches position 5,4.

![vectorsAddition](vectorsAddition.png)

## Vector Subtraction

Vector subtraction can be used to get the direction of one object from another.

Consider the following picture. Two objects exist at two different positions (a and b) and you want to calculate the direction that the second object (at position b) must face in order to the looking at the object at positon a. Using their individual positions, you can perform the calculation b-a to be given a vector.

Note that depending on the order in which the subtraction occurs, you will have different vectors. b-a and a-b have the same magnitude, but point in opposite directions.

![vectorsSubtraction](vectorsSubtraction.png)

## Dot Product

> [!tip] The dot product is a term to determine how two vector's directions relate to each other.

This is important because it describes the positioning of two vectors in relationship to each other. For instance, you can find out if two vectors are "facing" the same direction as each other.

If both vectors are facing the same way, the dot product would be 1

If they are perpendicular, the dot product would be 0.

If they are facing away from each other (or facing each other), the dot product would be -1.

![vectorsDotProduct](vectorsDotProduct.png)

## Cross Product

> [!tip] The cross product creates a new vector which is perpendicular to the two given vectors.

One example of why you may want this is to calculate the vector in which to rotate an object based on it's x and z position in the 3d space.

For instance, let's say you wanted to have a sail on a boat that is attached to the mast and it needs to be fully opened against the wind. You would have the vector relating to the mast and the wind, and the sail's vector should be perpendicular to both of those. So (refer to the image below), the cross product of the mast's (M) vector the wind's (W) vector would give the vector to set the sail (S).

This site goes into more detail: [http://blog.wolfire.com/2009/07/linear-algebra-for-game-developers-part-2/](http://www.google.com/url?q=http%3A%2F%2Fblog.wolfire.com%2F2009%2F07%2Flinear-algebra-for-game-developers-part-2%2F&sa=D&sntz=1&usg=AOvVaw2xTPfecIdNAVLTc55l-uhx)

![vectorsCrossProduct](vectorsCrossProduct.jpg)

## Vector Arithmetic

This video shows Vector Arithmetic in unity very well as well as the dot and cross products. While the video discusses the Unity game engine, the theory is the same for Godot.

![https://www.youtube.com/watch?v=e3z91RqZPAk&ab_channel=Unity](https://www.youtube.com/watch?v=e3z91RqZPAk&ab_channel=Unity)

## More Info?

If you would like more information, or want to study these topics in more depth, you can look at the vector cookbook here:

[https://docs.unity3d.com/Manual/VectorCookbook.html](https://docs.unity3d.com/Manual/VectorCookbook.html)

![vectorsMenu](vectorsMenu.png)