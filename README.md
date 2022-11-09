# Unity Boids! - Boid Simulation

A Boid Simulation that models real world flocking behaviour, built using Unity 3D. Not familiar with Boids? [Get started here](http://www.red3d.com/cwr/boids/)!

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See Installing for notes on how to deploy the project on your system.

### Prerequisites

[Unity 3D Version: 2017.4.1f1 Personal](https://unity3d.com/get-unity/download/archive)

### Installing via custom package

Follow the step by step instructions provided by the Unity installer for your desired system.

```
Note: This project was developed using 2017.4.1f1 Personal. While other Unity builds will likely work, this project has only been tested using this version.
```

Once Unity is installed on your machine, create a new Project.

With the new project open, navigate to "Assets > Import Package Custom package".

```
Included in this project submission is a unity package file named BoidSim Source Code.unitypackage
```

In the Custom package import screen, navigate to the downloaded Boid Simulation project directory.

Select and import "BoidSim Source Code.unitypackage".

The [project window](https://docs.unity3d.com/Manual/ProjectView.html) should now show 3 new directories "Prefabs", "Scripts", "Sprites", as well as a new Unity Scene file "Boid Simulation.unity"

Selecting the Boid Simulation.unity file will load the project scene file, simply press the [play button](https://docs.unity3d.com/Manual/Toolbar.html) to run the simulation.

### Installing via Unity Project Folder

```
Note: Installing via Project Folder will preserve custom sorting layers. If you opt to import via custom package, you may see boid agents "Flying above" the GUI. However, these occulding boids should not interfere with any UI selections.
```

Follow the step by step instructions provided by the Unity installer for your desired system.

```
Note: This project was developed using 2017.4.1f1 Personal. While other Unity builds will likely work, this project has only been tested using this version.
```

Once Unity is installed on your machine, select "Open Project".

```
Included in this project submission is a compressed unity project folder named BoidSim Source Code.zip

All scripts can be found in BoidSim Source Code > Assets > Scripts
```

Unzip the project source code, and select the source code folder to open the project in Unity.

The [project window](https://docs.unity3d.com/Manual/ProjectView.html) should now show 3 new directories "Prefabs", "Scripts", "Sprites", as well as a new Unity Scene file "Boid Simulation.unity"

Selecting the Boid Simulation.unity file will load the project scene file, simply press the [play button](https://docs.unity3d.com/Manual/Toolbar.html) to run the simulation.

### Running The Simulation

Upon execution of the Boid simulation (either via Unity editor, or simply running the applicable executable for your platform found in zipped Executables), you will be presented with a suite of small red equilateral triangles. Each one of these red geometric shapes represents a unique boid agent.

```
Each boid agent has its own instance of the Boid class running. This Boid class provides the core logic for which the boid will operate on.
Included are methods for the [three core flocking behaiours outlined by Reynolds](https://www.red3d.com/cwr/papers/1987/boids.html.) Alignment, Separation, and Cohesion.
In addition, contains methods for updating position & boudining a boid, and setting custom behavior thresholds.
```

These boids will immediately begin operating on their three core behaviours, in order to produce an ¨emergent flocking” behavior, similar to a school of fish, or a flock birds.

```
Core Behaviours:
* Alignment: Each boid agent steers toward the average heading of nearby boids
* Separation: Each boid agent steers away from any nearby boids
* Cohesion: Each boid agent steers toward the average centroid position of nearby boids

```

Each of these three behaviors can be then be modified and tailored by the user through the added GUI parameter settings menu displayed on the upper left
Additionally, the GUI allows for the instantiation of additional boids at runtime.
```
For instance, the effect of behaviour scaling is best visualized when multiple conflicting behaviours have equal range values,
providing a stronger scaling to one over the other should result in a visual behaviour bias
```
Finally, setting both range and scale threshold values for a behaviour to 0, will effectivly "turn off" that behiaviour.

```
Range & scale threshold values are applied to all boids in the simulation at once, and cannot be applied on a case by case basis.
```
```
Note: Range slider (0.0 - 1.0), Scale slider (0 - 10)
```

## Built With

* [Unity](https://unity3d.com/) - Cross platform development engine
* [MonoDevelop](http://www.monodevelop.com/download/) - Development IDE, included with Unity

## Version

Last updated May 9th, 2018 by Zachary Sullivan

## Author

* **Zachary Sullivan** - [Zachary Sullivan](https://www.zacharysullivan.net/)

## Acknowledgments

* [Craig Reynolds](https://www.red3d.com/cwr/boids/) - 1986 boid simulation paper
* [Rodney Brooks](https://pdfs.semanticscholar.org/dc66/c15a005dd1a3a9f033769e7fbc3b943be188.pdf) - Subsumption paper
