---
author: Ryan Cather
date: 2024-06-09
priority: 1
order: 11
---

> [!note]- Prerequisites
> - The bullets and enemy have been created
> - the bullets fire.

Similar to the approach taken with the Player object, each enemy (or any other object with health) will have its own health that will need to be diminished for it to be destroyed.

> [!tip] Each object or enemy that you wish to take damage needs to be configured in the same way.

> [!note] The object taking damage will need to have a `CollisionShape3D` configured as a direct child of the root node.
> ![[enemyDamageChildNode.png]]

Open the `enemy.gd` script  - or the script attached to the object that you wish to take damage.

Add a simple `take_damage(damage_amount)` function to the script, which simply outputs a test message to ensure that the process works.

![[enemyDamageFunction.png]]

```gdscript
func take_damage(damage):
	print("ouch")
```

Run the game at this stage to test the collision.

![[enemyDamageDemo1.gif]]


> [!tip] You may find it useful to slow the bullets down to properly test, as can be seen in this example.


Add a global `health` variable at the top of the script and set the value to 100.

![[enemyDamageVarInit.png]]

```gdscript
var health = 100
```

Update `take_damage()` to reduce the amount of health, and then check if the health has reached zero. If so, then delete the object.

![[enemyDamageFunctionUpdate.png]]

```gdscript
func take_damage(damage):
	health -= 50
	if health <=0:
		queue_free()
```

Run the project and you should see the object be destroyed as health reaches 0.

![[enemyDamageDemo2.gif]]

> [!note] Remember this process can work for any damageable object in the game - enemies, walls, doors etc.

![[commonBlocks#Commit & Push]]