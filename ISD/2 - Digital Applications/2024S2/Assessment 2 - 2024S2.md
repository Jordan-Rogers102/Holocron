
> [!important] View the assessment on Google Classroom for specific details.

# Assessable Topics 

These are the details you are to cover in the topics in Assessment 2. More Specific Details will be added later in the document.

![assessment2Topics](ISD/2%20-%20Digital%20Applications/2024S2/_images/assessment2Topics.png)

## Project Overview

TBA

## Code

TBA

## Data

TBA

## Development Process

- Brief 2-4 sentence summary for each week of what that week of development involved
	- What did you add to the project?
	- How does your addition fit into the grand scheme of the project?
	- What new skills were required to make these additions?
	- Explain how previous learning and work contributed to your ability to complete this week or work.
<strong>Screenshots as evidence is always good</strong>
Remember this entire section is meant to amount to around 1000 words so if you have 10 weeks worth of development process those summaries either need to be combined or need to be ~100 words each.
This weekly summary may not work depending on your project. It may be worthwhile to use this scaffold to put into words what was done to complete the project. However you may want to reorder or combine sections depending on how it will be best displayed. 

Example (written for week 7 of the development process):
During the 7th week of the development process I was at the stage where the game would function with players able to shoot and eliminate enemy NPCs. The plan for this week was to implement a functionality that would keep track of how many enemy NPCs were left in the level. This would act as a win condition that I would add functionality to during the 8th week of the development process. To keep track of the number of enemy NPCs I needed to create `global.gd` which is where I would store the variables for tracking the number of enemy NPCs. I added the enemy scene to the group `enemy` and utilised the code `get_tree().get_nodes_in_group("enemy").size()` as a way to track the number of enemies remaining and assigned this number to the variable `current_score`. I displayed this number to the player by adding `$Camera3D/playerScore.text = str()` to the physics function in the player script and had the function that caused enemies to die to reduce the variable `current_score`. With all of this working I can use the `current_score` variable as a way to trigger win conditions so that the game knows when all of the enemies have been eliminated and therefore knows when to progress to the next level.
## Technical Analysis

TBA

## Work Skills

TBA