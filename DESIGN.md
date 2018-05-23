## Boid Simulation Design Document

### PROJECT SUMMARY AND SIMULATION OUTPUT

For the CS50 term project, I intend to re-interpret in Unity3D using Object Oriented design principles, an artificial life simulation based on the 1986 flocking boids program developed by [Craig Reynolds](https://www.red3d.com/cwr/boids/).

```
Here the term “boid” is shorthand for “bird-like object”.
```

In the simulation, each boid agent navigates through a 2D environment, adhering to three mandatory subsumed behaviors:
```
	Alignment: Each boid agent steers toward the average heading of nearby boids
	Separation: Each boid agent steers away from any nearby boids
	Cohesion: Each boid agent steers toward the average centroid position of nearby boids
```
Each of these three behaviors can be modified and tailored by the user through parameter settings - for example, in regard to the minimum distance to maintain between boids, as well as a scaling factor by which each parameter is multiplied. Upon finalization of these factors, a summation of each of the aforementioned behavior vectors is calculated and used to update the boid’s acceleration vector.

This revised acceleration vector is then applied to the boid’s current velocity, which in turn is used to update the boid’s position in the world with each time step of the simulation.
Upon execution of the simulation, the three basic rules, as described, provide each individual boid with a unique vector which it uses to navigate through its environment.
This, in turn, produces an ¨emergent flocking” behavior, similar to a school of fish, or a flock birds.


### WHY PURSUE THIS PROJECT CONCEPT?

While the subject area of Artificial Intelligence (AI) has not been closely covered in this course, I have a strong passion for both game development, as well as the application of AI to games.

In my final year of my undergraduate Bachelor of Information Technology program I created a Unity3D game called "Valence". This game was developed using C# and [leveraged the use of subsumption-based AI characters (similar to the popular game The Sims)](https://www.zacharysullivan.net/internal-afsm-architecture)

Additionally, the concept of an artificial life simulation is one that I believe aligns closely to the intended challenge and project scope expected of CS50 students.
Furthermore, as a student currently enrolled in both CS50 as well as CSCIE-10b, I opted to use this opportunity to leverage material covered in both courses.
Additionally, the finalized boid simulation provides a particular interesting example of emergent behavior, whereby complex macro behavior can arise from the interaction of simple localized behaviors.

### INTERNAL BOID LOGIC

This project features a dynamic sized population of boid agents (visible as a simple red equilateral triangle) navigating around a fixed environment. The behavior of each boid agent is reliant on the position and velocity of each nearby agent which, in turn, influences the amount of steering force applied by each of the agent’s core behaviors (Alignment, Separation, and Cohesion).


Each individual boid has direct access to the x, y position & velocity of all boids in the environment. However, the execution of each behavior requires that the currently active boid only reacts to fellow boids within a certain radius around itself.

```
It is to be noted that each behavior has its own unique radius, modifiable by the user at run-time (Range Sliders).
```

The grouping of fellow boids is characterized by a distance (measured from the center of the boid to all other boids) and a velocity (the vector by which the boid is currently traveling). Boids found outside this group are therefore ignored and not considered by the three core behaviors. This dynamically sizable grouping can be imagined as region by which boids can influence one and other.

```
Or as Reynolds proposes “… a model of limited perception (as by fish in murky water) …”
```

Each boid object contains a unique instance method for the three core behaviors. These behavior methods return a two-dimensional vector to modify the boids trajectory.
With each time step, the boid’s velocity is updated to reflect the change in trajectory. By allowing the user to modify the behavior parameters, the simulation can selectively place emphasis on one behavior over another. This algorithm implementation, in accordance with Reynold’s original proposal, produces an emergent flocking behavior, visible as boids grouping together, and splitting away as they move about the environment.

### ORIGINAL BEST-CASE OUTCOME & FINALIZED PROJECT OUTCOME
##### WHAT I BELIEVE COULD ACCOMPLISH VS WHAT I DID ACCOMPLISH

The project proposal contained an outline for a boid simulation featuring both a simple GUI allowing the user to add additional boids to the population size, as well as the ability modify the color and Alignment, Separation, and Cohesion thresholds.

In the proposal, a window, would display a simulation showcasing the user-specified number of boids navigating around the environment.
These boids would in turn adhere to the three basic rules of flocking, and when executed will produce an emergent flocking behavior.

The final implementation features both a simple GUI as well as a boid simulation display. The GUI allows for the instantiation of additional boids, as well as the ability to modify the Alignment, Separation, Cohesion scale and range behavior thresholds.
The proposal mentioned the inclusion of a boid color changer, however the final implementation demonstrated there was a limited range of acceptable colors
from which the boids could be distinguished from one another.

```
For instance, red boids were easier to distinguish from one and other, versus blue or yellow boids.
```

## CLASSES & METHODS UTILIZED

Boid Class
Contains the core logic for a boid agent, included are methods for Alignment, Separation, and Cohesion behaviors, as well as methods for rendering a boid, and setting custom behavior thresholds.
```
1. Awake ()
    * Ceates a new boid at a random position somewhere in the environment, initialized with defaulted values for all behaviors.
2. getVelocity ()
    * Returns the velocity of the current boid
3. setSepScale (float scale)
    * Set this boid’s separation behavior scaling factor
4. setAlignScale (float scale)
    * Set this boid’s alignment behavior scaling factor
5. setCohScale (float scale)
    * Set this boid’s cohesion behavior scaling factor
6. setSepRange (float range)
    * Set this boid’s minimum distance by which a new separation behavior is calculated
7. setAlignRange (float range)
    * Set this boid’s minimum distance by which a new alignment behavior is calculated
8. setCohRange (double range)
    * Set this boid’s minimum distance by which a new cohesion behavior is calculated
9. run (Arraylist <Boid> boids)
    * Iterate through each boid in the simulation, and update the current boid’s core behaviors, based on the current distance to all other boids
10.	applyForce (Vector2D force)
    * Applies a new two-dimensional force vector to this boid’s current acceleration vector
11.	updatePos ()
    * Update this boid’s position in the simulation. Adds this boid’s current acceleration to its velocity, scaling either if the vector exceeds an arbitrary threshold. Finally, this boid’s velocity is applied to compute its new position, and its acceleration is reset.
12.	boundPosition ()
    * Bound the boid position in the environment, if the boid surpasses the environment bounds, wrap the boid around to the opposite side
13.	separation (Boid boid, double dist)
    * Follow Reynold’s outline of separation, by calculating and returning a new two-dimensional vector pointing away from the input boid. This method is repeatedly called for each boid within the separation range.
14.	alignment (Boid boid, int count)
    * Follow Reynold’s outline of alignment, by calculating and returning a new two-dimensional vector pointing towards the same heading as the input boid. This method is repeatedly called for each boid within §the alignment range.
15.	cohesion (Boid boid, int count)
    * Follow Reynold’s outline of cohesion, by calculating and returning a new two-dimensional vector pointing towards the average heading as the input boid. This method is repeatedly called for each boid within the cohesion range and is averaged across each boid called.
16.	OnCollisionEnter2D (Collision2D collision)
    * Checks if this boid has collided with any other gameobjects containing collider components
```

BoidController class
Contains logic for initial spawning of boid population, as well as adding & removing boids to/from the population list. Included are methods for spawning boids, recording all boids in a list, as well as setting the user defined Alignment, Separation, and Cohesion threshold values.

```
1. Start ()
    * Spawns an initial population of boids
2. addBoid()
    * Add a boid to the population list
3. removeBoid()
    * Removes a boid from the population list
4. update()
    * Iterate through each boid in the boidList and update their state
5. updateSepRange(float range)
    * Iterate through each boid in the population and update its minimum seperation range threshold
6. updateAlignRange(float range)
    * Iterate through each boid in the population and update its minimum alignment range threshold
7. updateCohRange(float range)
    * Iterate through each boid in the population and update its minimum cohesion range threshold
8. updateSepScale(float scale)
    * Iterate through each boid in the population and update its seperation scaling threshold
9. updateAlignScale(float scale)
    * Iterate through each boid in the population and update its alignment scaling threshold
10. updateCohScale(float scale)
    * Iterate through each boid in the population and update its cohesion scaling threshold
```

SliderController class
Contains logic for setting user defined Alignment, Separation, and Cohesion threshold values, as well as the ability to spawn additional boids

```
1. Start ()
    * Obtain and assign the corresponding UI components from the respecting parented GameObject, storing the current value of each slider
2. addEventListeners()
    * Applies a listener to each UI compnent, updates the corresponding textfield to display the current slider values
3. update()
    * Checks if the user has performed a left mouse click
4. update()
    * Iterate through each boid in the boidList and update their state
5. spawnBoid()
    * Spawns additional boids in the boidcontroller class
6. OnMouseUp()
    * Checks if any of the slider values have changed from their last saved states
```


