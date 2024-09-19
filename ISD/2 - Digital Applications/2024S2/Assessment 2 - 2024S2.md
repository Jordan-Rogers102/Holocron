
> [!important] View the assessment on Google Classroom for specific details.

# Technical Report

For suggestions on how to structure your report, see this page:

[Technical Report Writing](_sharedContent/technicalReportWriting.md)

# Assessable Topics 

These are the details you are to cover in the topics in Assessment 2. More Specific Details will be added later in the document.

![assessment2Topics](ISD/2%20-%20Digital%20Applications/2024S2/_images/assessment2Topics.png)

![[_sharedContent/Assessments2024S2/Task 2#Project Overview|Task 2]]

![[_sharedContent/Assessments2024S2/Task 2#Code|Task 2]]

![[_sharedContent/Assessments2024S2/Task 2#Data|Task 2]]

![[_sharedContent/Assessments2024S2/Task 2#Development Process|Task 2]]

Example: 

For the project there are 3 main components that needed to be created from a development standpoint. Those 3 components were the Environments, Player, and Enemies. While other components were required the remaining components were for the most part a result of developing the 3 main components.

To create these components a simple development loop was used where a feature of the component was created and tested in a safe environment. Once all components were completed and tested to the current stage of the project then work would begin on the next component or next addition to the project. The process of creating and testing begins with the identification or MVP requirements. There was a focus on keeping this identification minimalistic both to save time and to provide as blank a canvas to test as possible. In this way the functionality of the game was paramount and this development process would ensure that the functionality of the game was basic enough to run to completion and anything added for the purposes of flavour and gameplay complexity would not have an effect on the functionality of the game. Effectively with the creation of a safe-enclosed environment all the features of the game could be tested before the process of designing an interesting and fun levels began.

As an example of this development process, after a texture-less grey box was created to serve as a mechanic testing ground the creation of the player-model and the implementation of their movement, collision, and shooting began. For the player-model the basic MVP requirements were identified as:
- Being able to move, sprint, and jump around the environment.
- Being able to shoot.
- Having some collision with the environment in order to prevent falling through the walls and floors.
 A player was created as a formless, texture-less, capsule-shape and given a `CollisionShape3d` for the purposes of movement and detection. A `Camera3D` was attached to the player model at the appropriate height through which the player will view the game and a `RayCast3D` was attached project forward both for detecting objects immediately in front of the player.
Movement was added to the `player.gd` script to allow for movement by defining speed and then adding variables that track input direction based on player inputs and then change the `velocity` of the player-model to the current speed in the direction that was input. This was tested in the environment along with a togglable speed increase to add a sprint functionality, a jump function that prevented continual escalation by checking if the player-model is on the floor. This all interacted with a statement that added gravity to the player-model to ensure they stay on the ground.
This formed the basis for the player-model and interactions with the environment. Raycasting was tested against the walls using a `print()` function to show when the walls and floors were in the raycast. A bullet model was created and a spawn point was created for the bullets to come out of the players camera along the raycast and similarly a `print()` function was used to test when the bullets collide with walls and floors.

All of these features were tested in the safe environment that was created. Some slopes were added to the environment to test movement along an incline as an additional test that was not identified during the MVP identification process. With this complete the project could continue knowing that the player would be able to move around the environment without falling through anything and that the bullets were being detected when colliding with objects (which would become relevant when implementing enemies).

Once all of the 3 main components were completely implemented and tested the game within the safe environment the game was ready to be iterated upon to introduce flavour and complete game design. First the levels were made more interesting with environments that better reflected the gameplay. With small maze-like structures to encourage a slow methodical progression and then some long catwalks to encourage a full on, fast-paced section. Textures were imported using seamless png images and applied to the environment. Royalty free enemy models were sourced from online and used to better represent the enemies.

Given that the primary functions of the game had been completely tested before the implementation of complex design there was an expectation that these kinds of issues may come up. Small changes to hit boxes of enemies were needed to better fit the new textures. Furthermore there were some locations in the levels that could be considered bugs. Where these were found small fixes were made in the environment design mostly by adding additional `CollisionShapes3D` that prevented access to those areas. There is an argument here for a more lateral development process that prioritises the game being designed and developed simultaneously where the functionality and flavour are tested together. This kind of process may be able to prevent the kinds of bugs that occurred when development and design occurred independently but in a solo project with a strict time constraint it is more efficient to hone in on the basic MVPs of the functionality rather than developing the functionality based on how it fits into the design.

When refining the game ready for submission there was an option to use Blender in order to create assets for the various in game models. The final product of the game has an almost discordant feeling due to the importation of assets that were created independently from one another. Creating assets from scratch or independently would have been an ideal solution to this issue. However time crunches and adherence to the strict MVPs of the project rendered this strategy inefficient and would have reduced the ability for the project to function as intended on the day of submission.  Furthermore animation was another 


![[_sharedContent/Assessments2024S2/Task 2#Technical Analysis|Task 2]]



![[_sharedContent/Assessments2024S2/Task 2#Work Skills|Task 2]]
