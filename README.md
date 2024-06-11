# Team_VirtualVamguard_RVCE_Meta
SRIB-PRISM Program

## Overview
Medical professionals face challenges in accurately visualizing and diagnosing conditions based on traditional 2D images from MRI and CT scans. The lack of depth perception can impede precise understanding of anatomical issues. "MediScan 3D" will provide an immersive 3D VR experience that transforms 2D medical images into a spatial representation. Doctors can visualize and analyze the patient's anatomy in three dimensions, enhancing accuracy in diagnosis and treatment planning.


## Features
Threshold-Based Surface Detection:
The method involves identifying voxels with a density higher than a
specified threshold, representing the surface of interest within the
volume.

Raymarching Technique:
 Rays are cast from the eye (camera) through the volume,
 progressing voxel by voxel.
 The process stops when a voxel exceeding the threshold density is
 encountered, determining the surface point for that ray

 Initial voxel check:
 Begins raymarching either from the eye or ideally from where the
 ray intersects the front face of the bounding box containing the
 volume data.
 
  Basic Implementation:
 The algorithm is straightforward and easy to implement, focusing
 on detecting and rendering the first voxel above the density
 threshold
 
 Diffuse Lighting Enhancement:
 A diffuse reflection lighting significantly improves the visual
 quality by simulating light reflection on the surfaces.
 Diffuse lighting considers the angle between the light source and
 the surface normal, creating a more realistic appearance by
 highlighting surface features and giving a sense of depth.
 
 Surface Normal Calculation:
 To apply lighting, the surface normal at each voxel is computed,
 which is essential for determining how light interacts with the
 surface.
 Surface normals can be estimated by analyzing the gradient of the
 voxel density values
 
 
## Getting Started

### Prerequisites
Unity 2020.3 or later
Windows, macOS, or Linux operating system
Basic knowledge of Unity and C# scripting

### Installation
Clone the repository:

sh
Copy code
git clone https://github.ecodesamsung.com/SRIB-PRISM/Team_VirtualVamguard_RVCE_Meta
### Open the project in Unity:

Launch Unity Hub.
Click on "Open" and navigate to the cloned repository folder.
Select the folder and open the project.

### Install necessary packages:

Open the Unity Package Manager (Window > Package Manager).
Install any recommended or required packages listed under "Dependencies" in the project.
## Usage
Import X-ray Image:

Place your X-ray image file into the Assets/Resources/XrayImages folder.
The image should be in JPEG, PNG, or DICOM format.
Load and Convert:

Run the scene named MainScene.
Use the UI to load your image from the dropdown menu.
Click the "Convert to 3D" button to start the reconstruction process.

## Interact with the 3D Model:

Use mouse or touch controls to interact with the generated 3D model.
Adjust visualization settings via the settings panel.

## Our Approach
#VOLUME RENDERING:
A technique used in computer graphics and scientific visualization to display a three-dimensional dataset. Here we used results of CT scans and MRIs as these scans produces a 3-dimensional dataset, where each cell defines the density at that point. This 3D voxel data from these scans nicely into a box, so we render a box and use raymarching to fetch the densities of each visible voxel inside the box

Here we incorporated 3 rending techniques for determinig the colour
 of the output :
 1.Maximum intensity projection
 2.Direct volume rendering
 3.Isosurface rendering
 
 1.Maximum Intensity Projection- This is the simplest of the three techniques. Here we simply draw the voxel (data value) with the highest density along the ray. The output colour will be white, with alpha = maxDensity.
 ![image](https://media.github.ecodesamsung.com/user/30579/files/a2ba724e-1671-489c-a7b2-432b2d4d5ed2)
 
 2.Direct Volume Rendering with compositing- This is probably the most advanced of the thress techniques. However the basic idea is this: On each step, combine the current voxel colour with the accumulated colour value from the previous steps.
 
We linearly interpolate the RGB values, like this: newRGB = lerp(oldRGB, currRGB, currAlpha). And then add the new alpha to the old alpha multiplied by (1 – new alpha). col.rgb = src.a * src.rgb + (1.0f src.a)*col.rgb; col.a = src.a + (1.0f – src.a)*col.a;
![image](https://media.github.ecodesamsung.com/user/30579/files/3eaf8608-f172-4515-bcc3-b1470db87162)

3.Isosurface Rendering- The most basic implementation of isosurface rendering is quite simple: Draw the first voxel (data value) with a density higher than some threshold. Now we need to start raymarching at the eye (or ideally at the point where the ray hits the front face of the box) and move away from the eye. When we hit a voxel with density > threshold we stop, and use that density. This is simple to implement, but if you try it you might be disappointed by how bad the result looks. However, if we add some lighting it will look a lot better. Lighting Since we are rendering the surfaces only, we need light reflection to make it look good. For our example we will only use “diffuse” reflection

![image](https://media.github.ecodesamsung.com/user/30579/files/b53e0d67-717a-474c-8a5e-b01a67118912)
![image](https://media.github.ecodesamsung.com/user/30579/files/418bc9ad-6f48-41c7-9c25-5782c72286c6)

## Image Examples:

#User Interface
![WhatsApp Image 2024-06-05 at 06 21 39_cf9f53ae](https://media.github.ecodesamsung.com/user/30579/files/ec8f3248-b6ab-445a-b038-7b614b63e130)
![WhatsApp Image 2024-06-05 at 06 22 04_baa8610b](https://media.github.ecodesamsung.com/user/30579/files/fcce0437-3fd8-4999-96d7-2ff9d5a1d720)
![WhatsApp Image 2024-06-05 at 06 22 37_bcf59df3](https://media.github.ecodesamsung.com/user/30579/files/9953f967-3823-4e57-91ab-627dfa9d2339)
![WhatsApp Image 2024-06-05 at 06 23 17_0d84fc7c](https://media.github.ecodesamsung.com/user/30579/files/612089b9-a5d7-4b2d-99f0-65bf76b19350)
![WhatsApp Image 2024-06-05 at 06 23 53_8c101a72](https://media.github.ecodesamsung.com/user/30579/files/5bd75f0a-7446-4e52-81b1-e4877c86928c)

#image conversion
<img width="662" alt="image" src="https://media.github.ecodesamsung.com/user/30579/files/652d48c5-6283-49b3-acbd-bb74d2f13148">
<img width="674" alt="image" src="https://media.github.ecodesamsung.com/user/30579/files/7bea8e4e-1f22-404a-a12a-ef6e24a898db">
![image](https://media.github.ecodesamsung.com/user/30579/files/aa793547-7511-4811-a006-fefc23d9347c)
![image](https://media.github.ecodesamsung.com/user/30579/files/df34f671-02ca-485a-b30b-e038d29595de)


## Acknowledgements
Thanks to the Unity community for the invaluable resources and support.
Inspired by existing medical imaging tools and technologies.
