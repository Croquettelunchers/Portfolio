[About Me](index.md) | [Projects](Projects.md) 

# VFX

# Interior Shader

<img src="Projects/InteriorShader/InteriorsShader4.jpg" alt="BuildingCapture" style="height: auto; width: auto">   

Interior shaders, also called fake interiors, are a rendering technique using multiple parallaxed UV coordinates to simulate depth.
This particular shader features **atlassed textures**: all of the different interiors are compacted on a single, interchangeable "collection" texture of variable size. The curtains are featured on a separate collection. Both of these allow us to adapt to different architectural styles.

> Per NDA, I cannot show you the code of this shader. It was prototyped using **Amplify Shader** and then rewritten in **HLSL** with some adaptations for real-time global illumination (à-la Lumen).  
> The feature is complemented by an automated mapping tool spreading UV into select **udims**

I call them UV-based interiors. The distinction is important because they become much more functionnal if their projection coordinates aren't raw world-space passed as UV, like Triplanar functions do. These need to react to the world *localy* and *by-surface*. 

We achieve this by using the right projection matrix: **WorldToTangent** and multiplying it with our **WorldPosition**, then we divide this with fractionnal parts (**frac**) of our **Vertex Coordinates**, all that's left at this point is to **DDX() DDY()** the previous result. DDX and DDY effectively compare the variations between neighboring pixels and, if done right, ultimately provide us with fully turnable and rotatable surfaces.  

<img src="Projects/InteriorShader/DDXDDY.PNG" alt="DDXDDY" style="height: auto; width: auto">  

<br/>

<img src="Projects/InteriorShader/BuildingCapture.jpg" alt="BuildingCapture" style="height: auto; width: auto">  
<span style="color: gray;">The effect needs to remain convincing at all hours during the simulation.</span>  

Notice how the appartments on the extremities of the building are see-through. This is achieved using reserved udims.

The very first iteration of the shader used a color map for randomization and coloration but even a big color map wasn't sufficient; humans are too good at pattern recognition.
So I rounded down multiple single-channel noise generators to produce truly convincing random patterns.

<img src="Projects/InteriorShader/InteriorShader3.gif" alt="BuildingCapture" style="height: auto; width: auto">  
<br/>
<img src="Projects/InteriorShader/InteriorShader.gif" alt="BuildingCapture" style="height: 260px; width: 400px">   

Here's a more in-depth rundown of what the shader can do:

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/InteriorShader/UV-BasedInteriorMapping.mp4" type="video/mp4">
</video>



## Waterfall and Fountains

I was mandated to produce fountains and a waterfall for one of Smartpixel's app.  
The fountains and splashes are standard shuriken particles with depth-fading and a 4-frame animation etched at the speed of light in Krita  
Both use some custom normal-handling equations for slightly more consistantly plausible tints for when they're lit vs under the shade.  

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/Waterfall.mp4" type="video/mp4">
</video>
<p style="color: gray;">Final version</p>

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/WaterfallProto.mp4" type="video/mp4">
</video>
<p style="color: gray;">Prototype version with additionnal foaming and tweaks</p>

My reference was foaming, clumping, and flowing faster on the sides which I attempted to reproduce to the best of my capacities. 

## Firepit

This fire VFX was designed specificaly for firepits. It is textured in worldspace offering ease of scalability and constant aspect for its texture.
It is composed of 5 quads. 2 for both the X and Z axis and another one facing upwards.  

It's important to note that these projects' lux range varies from ~50lux at night to ~150 000lux at day as they are using physicaly-based light ranges. With this level of variation, most emissive vfx and world-space UI shaders need some degree of adaptation.  

This version of the shader was conformed to Smartpixel's real estate needs: a cozy flame, with a clean rich-feel, minimal smoke and no unruly embers.

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/DancingFireSeq.mp4" type="video/mp4">
</video>
<p style="color: gray;">Final version</p>

This one is still under development, it features particles for embers, thicker smoke and an extra camera-facing quad for heat deformation.  

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/DancingFire.mp4" type="video/mp4">
</video>
<p style="color: gray;">WIP version with new features</p>

Notice the light variations, I am using a regular point light with a script I've written that moves it erraticaly and changes its intensity over time.  
Coupled with it, I am also working on a shader feature that ultimately would work as a shrink-wrap decal making use of Unity's animatable voronoi noise to add an organic touch to the light, bringing us closer to the dancing shadows that a firepit casts.  

For the time being, it's in the form of a global-parameter feature applied on the neighboring surfaces. It will be so until I start working on the decal system.
 
<img src="Projects/VFX/DancingFireShadeController.PNG" alt="" style="height: auto; width: auto">  
<span style="color: gray;"></span>

<img src="Projects/VFX/FlickeringLight.jpg" alt="" style="height: auto; width: auto">  
<span style="color: gray;"></span>

<img src="Projects/VFX/FlickeringLightCode.PNG" alt="" style="height: auto; width: auto">  
<span style="color: gray;"></span>

<img src="Projects/VFX/FlickeringLight.PNG" alt="" style="height: auto; width: auto">  
<span style="color: gray;"></span>

## Automatic Colorizer

Automatic Colorizer is a shader feature that randomizes props' colors depending on their world position. It's a neat trick to add variations for ***static*** foliage and any prefab that appears repeatedly in the background.  
Otherwise, the color could be applied dynamicaly on-spawn if the cars were animated. Preferably through vertex color as this allows to preserve a single draw call for the lot.
This one is handling colors only but it's possible to distort meshes and create all manners of variations without introducing new draw calls in the render queue.
This specific case is sampling a micro 16x16 texture to use as color palette, which still provides 256 variations. 

<img src="Projects/VFX/Cars.gif" alt="" style="height: auto; width: auto">  
<span style="color: gray;">The Car shader also has a nice shellac material, but this on-the-fly gif does it no justice</span>

## Item Box 

I produced this item box by doing as much as I could in-shader as a fun lightweight challenge.  
the dots and their normals are mathematical equations.   
the exclamation mark is a texture though, but its look-at constraint and its animation are done in-shader.  
the transparency quality, sorting and layering is guaranteed using vertex color to differentiate the external surface from the internal one.  

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/MysteryCube.mp4" type="video/mp4">
</video>
<p style="color: gray;"></p>

## Autochamfering

Autochamfering was a crutial upgrade to our Archviz projects, Unchamfered edges are a well documented realism-killer.  

There are essentialy 3 rationnal ways to do auto-chamfering; 
- dedicating a UV channel for it and scripting a tool to map out the object's vertices onto virtual shapes.
- using a guide texture 
- using a post-process that is very similar to occlusion in principle and execution.

Our pipeline was still using channel-packed textures so my solution was to put to work an unused alpha channel to use as a guide texture. 
This solution is both quick to implement and to execute for people in production.

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/EdgeMapping.mp4" type="video/mp4">
</video>
<p style="color: gray;"></p>

# UI

## Motion design

> Using a collection of vertex-colored meshes, a quad, a circle, a square, an hex and a triangle, in tandem with a dedicated shader, I produced a variety of motion design animations.

Check out the following videos for examples for custom UI FX requests in application.


<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/UIReticle2.mp4" type="video/mp4">
</video>
<p style="color: gray;">Armored Core-style reticle</p>

### Pins
These are sample animations for World-space positionned pins, as you press on them they deploy to reveal information.  
Typically, these designs share a base set of common animation "rules" such as expansions, shapes completions, fades, etc. 

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/LozengePin2.mp4" type="video/mp4">
</video>
<p style="color: gray;">Configuring these pins takes about 15 minutes to 30 minutes</p>  

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/HexPin.mp4" type="video/mp4">
</video>

So, combining multiple rudimentary shapes: Quads, Circles, Hexes, Squares and Triangles, we can quickly produce a variety of dynamic UI pins and gizmos. All using the same tool.  

## Smartpixel's "VFX shader"

While working on the Comcast project [Comcast: 3D Interactive Tour of a Digital City](https://www.youtube.com/watch?v=8_HSRpEftAk), the client's various demands forced me to dramaticaly improve our sci-fi shading capacities. Resulting in a single all-encompassing shader covering around 90% of all Smartpixel's custom shading needs.  

Smartpixel's "VFX shader" features: 
- In-shader switches to completely toggle features for performances.
- Depth fading
- Render-on-top
- UV, World-space or Screen-space fading
- Nighttime/Daytime colors 
- Texture scrolling
- Thickness adjustment through displacement
- Vertical dissolution
- RGB-HSV coloring
- Non-overlapping transparency

Due to the inherent complexity of the shader, I have prepared many sample prefabs for the team to help them quickly setup various effects  

Here are a few presets for what we called "ghost buildings" which were future phases or interractive elements in the background. 

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/GhostBuildings.mp4" type="video/mp4">
</video>
<span style="color: gray;"></span>

The same shader also works for transport lines, splines used to illustrate busses, subway, pedestrian paths etc. 

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/TransportLines.mp4" type="video/mp4">
</video>
<span style="color: gray;">Various versions of transport lines and how they could display through other elements</span>
