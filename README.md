# Unity-Tools
This repository contains the modular systems I developed in Unity whilst working on an unreleased title called Tethr. The tools are designed to work with both 2D & 3D Unity projects.


***


# Surface Aligner

A utility package intended to be used for easily aligning objects to surfaces both in the editor and at runtime. The utility aims to drastically decrease the time spent on level design, preventing developers from having to manually align every instance of an object to certain surfaces. The utility works for both **2D** and **3D** projects.

Within **Tethr** the utility will largely be used to align walkable enemies to the ground to ensure that visually they appear to be standing and walking on the ground even though they have no rigidbodies.

The utility is fully commented, therefore if you are still unsure about anything even after reading the documentation, you can check out the source code to get a deeper insight.


## Editor Use

The **Surface Aligner** features custom _**Project Settings**_, which you can access via the **Unity Editor** by going to **Edit** > **Project Settings** > **Surface Aligner**. 

<p align="center"><img width="869" height="678" alt="Surface Aligner Project Settings" src="https://github.com/user-attachments/assets/ee41b97b-aed0-48d8-b4f5-c65b534fc175" /></p>

Here you will be able to customise various editor-side aspects of the utility such as the gizmo settings, as well as more importantly the **Surface Checks**, which allow you to define custom alignment rules per prefab, such as the direction you want the alignment check to occur in or what surfaces you want to check for, using a layer mask. 


### Functionalities

- A surface check is run in the editor whenever you drag an object in the scene that comes from one of the prefabs noted in the **Surface Checks**.
- As you drag the object around, gizmos are drawn, which show you the potential location that the object will align to upon releasing the object.

<p align="center"><img width="203" height="265" alt="Gizmo Visuals" src="https://github.com/user-attachments/assets/ef677bf2-5173-47e1-a9e3-30bd12b65596" /></p>

The **yellow** line in the image tells you how the object will be oriented when it is aligned to the surface.

- When you release your **LMB** after dragging, the object will be automatically aligned to the surface.

<p align="center"><img width="193" height="223" alt="Aligned Object" src="https://github.com/user-attachments/assets/47b073ed-8739-4e9f-b550-c74ffaf5fdcd" /></p>

- The utility also supports alignment and visualisation for multi object selections.

<p align="center"><img width="390" height="370" alt="Multi Object Selection" src="https://github.com/user-attachments/assets/75cb5abf-1872-4a50-b69b-41a34102b546" /></p>

- Further object preview visualisation is also provided allowing you to see how the object/s will be aligned.

<p align="center"><img width="363" height="277" alt="Object Preview" src="https://github.com/user-attachments/assets/a573804e-f96e-4576-8c65-5c2373873033" /></p>

- To circumvent automatic surface alignment on objects noted inside **Surface Checks**, you can either remove them from the list or move them manually via the **Transform** component.

- The editor-side functionalities are automatically disabled during play to give more freedom to developers when testing gameplay, allowing them to move any object freely as they wish. These functionalities are then automatically re-enabled upon exiting play mode.


## Runtime Use

The editor-side of the package already utilises transform extension methods for surface alignment, therefore if you want to perform surface alignment without relying on the editor, you can just call the extension methods in your own code. Make sure you include "**namespace Tethr.SurfaceAligner**" at the top of your file to gain access to the extension methods.


### Extension Methods

- **AlignToSurface** (3D) / **AlignToSurface2D** - Attempts to align the transform to the detected surface using the provided values.
- **GetSurfaceHit** (3D) / **GetSurfaceHit2D** - Attempts to get a valid surface hit via raycasting using the provided values.
- **AlignToGround** (3D) / **AlignToGround2D** - Helper methods that attempt to align the transform to the ground (downwards) using the provided values.



***

# Path Visualiser

An editor-only utility package intended to be used for visualising paths. The utility aims to allow for easier path placement during level creation, as well as easier path visualisation during editor play mode. The utility works for both **2D** and **3D** projects and is intended to be used in editor-only contexts such as _**OnDrawGizmos**_ or _**OnDrawGizmosSelected**_.

Within **Tethr** the utility will largely be used to visualise enemy paths, with the potential of also being used to visualise paths of other objects such as moving platforms/traps.

The utility is fully commented, therefore if you are still unsure about anything even after reading the documentation, you can check out the source code to get a deeper insight.


## Requirements

The path visualisers example scripts require the [**EditorAttributes**](https://assetstore.unity.com/packages/tools/gui/editorattributes-269285) package to be installed to function properly, if you do not need the examples you can just delete them.


## Editor Use

The **Path Visualiser** features custom _**Preferences**_, which you can access via the **Unity Editor** by going to **Edit** > **Preferences** > **Path Visualiser**.

<p align="center"><img width="1101" height="578" alt="Path Visualiser Preferences" src="https://github.com/user-attachments/assets/cf7b4adc-63f7-45bf-a3b4-e3d767dde9ef" /></p>

Here you will be able to customise various editor-side aspects of the utility such as line, disc and label gizmo settings.


### Functionalities

The utility comes with two path visualisation methods, make sure you include "**namespace Tethr.PathVisualiser**" at the top of your file to gain access to the visualisation methods:

* **DrawPath** - Draws a path from the provided _**Vector3**_ points using a specific type of path traversal (**Once**, **Loop**, **PingPong**) with the ability to optionally provide previous and target point indices to visualise the currently active line segment (Green by default).

<p align="center">
<img width="300" height="430" alt="DrawPath Once Visual" src="https://github.com/user-attachments/assets/a9e260ea-6fae-4165-9866-202885f11af7" />

<img width="300" height="430" alt="DrawPath Loop Visual" src="https://github.com/user-attachments/assets/56fa029c-abd8-46ff-a12b-60eb650ec51e" />

<img width="300" height="430" alt="DrawPath PingPong Visual" src="https://github.com/user-attachments/assets/f40fac4f-b106-4e47-955e-cd95b07d8640" />
</p>

* **DrawTargetLine** - Draws a path from a current position (Marked with **C**) to the targets position (Marked with **T**).

<p align="center"><img width="432" height="360" alt="DrawTargetLine Visual" src="https://github.com/user-attachments/assets/19b81aa9-08a2-4e87-b376-2ca962c5388d" /></p>


### Examples

The utility also comes with two example _**MonoBehaviour**_ scripts called **PathVisualisationExample** and **TargetVisualisationExample** that users can add onto objects via the _**Inspector**_ to aid further in their understanding of the utility.



***

# Detection Visualiser

An editor-only utility package intended to be used for visualising detection areas. The utility aims to allow for easier configuration of detection related settings by actively visualising them in the editor. The utility works for both 2D and 3D projects and is intended to be used in editor-only contexts such as OnDrawGizmos or OnDrawGizmosSelected.

Within Tethr the utility will largely be used to visualise enemy detection areas.

The utility is fully commented, therefore if you are still unsure about anything even after reading the documentation, you can check out the source code to get a deeper insight.


## Requirements

The detection visualisers example script requires the [**EditorAttributes**](https://assetstore.unity.com/packages/tools/gui/editorattributes-269285) package to be installed to function properly, if you do not need the example you can just delete it.


## Editor Use

The **Detection Visualiser** features custom _**Preferences**_, which you can access via the **Unity Editor** by going to **Edit** > **Preferences** > **Detection Visualiser**.

<p align="center"><img width="1102" height="566" alt="Detection Visualiser Preferences" src="https://github.com/user-attachments/assets/3a4dc84a-5f6f-4052-b329-e73d0ca00db7" /></p>

Here you will be able to customise various editor-side aspects of the utility such as colour, alpha amount and line thickness.


### Functionalities

The utility comes with three types of detection visualisation methods, make sure you include "**namespace Tethr.DetectionVisualiser**" at the top of your file to gain access to the visualisation methods:

* **DrawRange** / **DrawRange2D** - Draws a spherical range visualisation (3D) / a circular range visualisation in the X-Y plane (Vertical Plane) (2D) using the provided centre position and radius, with the ability to optionally provide a _isTargetDetected_ bool that changes the colour of visualisation.

<p align="center"><img width="443" height="443" alt="Detection Visualiser Range Visual" src="https://github.com/user-attachments/assets/e356b28b-9e19-4853-9162-e10af97cf6e4" /></p>

* **DrawFieldOfView** / **DrawFieldOfView2D** - Draws a field of view visualisation in the X-Z Plane along with a supporting spherical wireframe outline (Ground Plane) (3D) / X-Y plane (Vertical Plane) (2D) using the provided centre position, angle of view, radius, with the ability to optionally provide a _isTargetDetected_ bool that changes the colour of the visualisation as well as the _rotation_ of the gameObject used to offset the field of view visualisation.

<p align="center"><img width="365" height="314" alt="Detection Visualiser FOV Visual" src="https://github.com/user-attachments/assets/a64f3ea2-1837-408f-9b5a-10b29040aaf7" /></p>

* **DrawBounds** - Draws a bounds visualisation using the provided centre position and size, with the ability to optionally provide a _isTargetDetected_ bool that changes the colour of the visualisation. This method can be used for both 2D & 3D instances.

<p align="center"><img width="301" height="302" alt="Detection Visualiser Bounds Visual" src="https://github.com/user-attachments/assets/f2d62602-aecf-47eb-9292-325bfd460faa" /></p>


### Examples

The utility also comes with an example _**MonoBehaviour**_ script called **DetectionVisualisationExample** that users can add onto objects via the _**Inspector**_ to aid further in their understanding of the utility.
