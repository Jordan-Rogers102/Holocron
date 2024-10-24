
# A*

A* (pronounced "A Star") is an algorithm used to calculate the most efficient route between two points. This algorithm is used in not only game development, but in GPS navigation systems to calculate how to get to a destination.

> [!question]- KEYWORDS
> Some keywords that you need to know before moving on:
> - **agent**: any object that is part of the algorithm. For instance, the player or the enemy.
> -  **node**: each "step" of the path towards the destination.
> - **edge**: The lines linking the nodes.
> - **cost**: how hard it is going to through that node. It could be the distance, the speed the agent moves (like a speed limit), or anything else that effects the time it takes to travel (such as traffic)

## Algorithm Overview
[Here](http://www.google.com/url?q=http%3A%2F%2Fwww.policyalmanac.org%2Fgames%2FaStarTutorial.htm&sa=D&sntz=1&usg=AOvVaw1bmf-du5DHTK4UcFQZn_xi) is a detailed analysis of the algorithm if you wish to read further.

[Here is another](https://www.google.com/url?q=https%3A%2F%2Fwww.raywenderlich.com%2F4946%2Fintroduction-to-a-pathfinding&sa=D&sntz=1&usg=AOvVaw2O3py6iEsGR_2FGRsENFiy)

[This site](http://www.google.com/url?q=http%3A%2F%2Fwww.redblobgames.com%2Fpathfinding%2Fa-star%2Fintroduction.html&sa=D&sntz=1&usg=AOvVaw32anRnylY5VqzntoT80zzT) goes through a number of path finding algorithms in detail, with some animation and simulations.

This video covers the algorithm and how the overall A* Pathfinding system works.

![https://www.youtube.com/watch?v=-L-WgKMFuhE&ab_channel=SebastianLague](https://www.youtube.com/watch?v=-L-WgKMFuhE&ab_channel=SebastianLague)

## A Practical Example

Consider this animation of a Unity Scene ([download here](https://drive.google.com/open?id=0B2BJHuQ5gr5QMl9CWGJDRi1HdGs) and import into your project). The player is in the bottom left tile. When the player clicks on another tile, the game has to calculate the most efficient route, whilst avoiding the walls.

The cost of moving to a standard tile is 1.

The blue section in the middle of the "world" represents water. There is an additional cost for the player to move through water tiles.

The algorithm calculates the path based on the cheapest cost to get from the start to the destination.

You'll notice that because of the additional cost involved, the algorithm avoids the water tiles as much as possible.

![aStarExample](aStarExample.gif)

## Overview

*Ignoring game development in general,* let's look at the problem that the algorithm is attempting to solve.

### Nodes & Edges

This image shows a grid of nodes (blue circles) to represent all possible paths between the start (S) and the desired destination (D).

What is the most efficient route? You could guess the path just by looking at the image, but **this is a logical representation** of the mesh of nodes. The distances between the nodes on the image is not to scale.

![aStarNodesEdges](aStarNodesEdges.png)

You have to consider the cost of each node and edge. Let's add those costs.

### Costs
In this version, you can see the costs (in green squares) of travelling each edge has been added. Now you have more data to use to calculate the most efficient path.

![aStarTravellingCost](aStarTravellingCost.png)


### First Guess

Looking at the red dotted line as the first guess, the cost of that path is a 1 + 3 + 2 = 6.

Which path is the most efficient?

![aStarFirstGuess](aStarFirstGuess.png)


### Solution?

Based on the costs of each travelling to each node, possibly the most efficient route is shown here.

The cost of the indicated path is 4.


![aStarSolution](aStarSolution.png)

> [!info] It's important to note that in the example above, there is only one cost listed for travelling each edge. In reality there can be many costs. If you consider a GPS navigation system, there would be traffic, speed limit, accidents, roadworks, number of traffic lights or roundabouts etc.
> The A* Algorithm can take any number of costs associated with the edges and nodes to find the most efficient path.

## Different Cost, Different Path

If the costs are different, the resultant path may be vastly different.

What's the most efficient path in this example?


![aStartCostChange](aStartCostChange.png)

## How Does the Computer Do It?

Humans can look at the information above and relatively quickly work out the best path, however computer are not that clever and they need to follow an algorithm to solve the problem.

The pathfinding agent (the "player" at the start point) first finds the nodes adjacent to it and calculates the cost involved. It then continues from each node, calculating the costs to the adjacent nodes.

Which node does it choose first? The one with the lowest cost.

### Stage 1

Given the cost of the edge from the starting node, the cost to get to the adjacent nodes is both 1.

![aStarStep1](aStarStep1.png)

### Stage 2

In this next step the next stage is calculated, using the nodes adjacent to the Stage 1 nodes.

With the path costs, it is now possible to prioritise some paths over another. As the algorithm doesn't know the cost further down the track at this stage, it can't dismiss any possible paths as yet.

The most efficient routes are the ones indicated by the arrows. They are prioritised because they have the lowest cost thus far.

![aStarStep2](aStarStep2.png)

### Stage 3+

The process continues calculating as many paths as required to reach the destination. It starts each stage with the lowest cost path to check if that path is more efficient than all other paths.

![aStarStep3](aStarStep3.png)
## Limitations Of A*

While A* is great for calculating a path between two set points, it struggles when the nodes are not static - i.e. when they move. The algorithm doesn't cater well for walls or obstacles that can move, because then the path has to be recalculated