[About Me](index.md) | [Projects](Projects.md) 

# VFX

## Waterfall

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/Waterfall.mp4" type="video/mp4">
</video>
<p style="color: gray;">Final version</p>

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/WaterfallProto.mp4" type="video/mp4">
</video>
<p style="color: gray;">Prototype version with additionnal foaming</p>

## Firepit

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/DancingFireSeq.mp4" type="video/mp4">
</video>
<p style="color: gray;">Final version</p>

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/DancingFire.mp4" type="video/mp4">
</video>
<p style="color: gray;">WIP version with new features</p>

<img src="Projects/VFX/DancingFireShadeController.PNG" alt="" style="height: 280px; width: auto">  
<span style="color: gray;"></span>

<img src="Projects/VFX/FlickeringLight.jpg" alt="" style="height: 280px; width: auto">  
<span style="color: gray;"></span>

<img src="Projects/VFX/FlickeringLightCode.PNG" alt="" style="height: 280px; width: auto">  
<span style="color: gray;"></span>

<img src="Projects/VFX/FlickeringLight.PNG" alt="" style="height: 280px; width: auto">  
<span style="color: gray;"></span>

## Item Box 

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/MysteryCube.mp4" type="video/mp4">
</video>
<p style="color: gray;">WIP version with new features</p>

## Autochamfering



There are essentialy 3 rationnal ways to do auto-chamfering; 
- dedicating a UV channel for it and scripting a tool to map out the object's vertices onto virtual shapes.
- using a guide texture 
- using a post-process that is very similar to occlusion.

Our pipeline was still using channel-packed textures so my solution was to use the alpha channel of one of them to achieve this result. 
This solution is both quick to implement and to use for people in production.

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/EdgeMapping.mp4" type="video/mp4">
</video>
<p style="color: gray;"></p>

# UI

## Next-Level User Experience

Every once in a while a client hits you with some Cyberpunk-grade "*this is an experience*" design.  
These, are, **AWESOME**. Often times they will feature extensive motion design added to their UI experience, with quirky animated gizmos or transitions.
Typically, these designs share a base set of common animation "rules" such as expansions, shapes completions, fades, etc.

Check out the following videos for examples for custom VFX requests in application.

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/UIReticle2.mp4" type="video/mp4">
</video>
<p style="color: gray;">Fire some missiles!</p>

Or a more typical transition animation, highly appreciated by clients :

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/LozengePin2.mp4" type="video/mp4">
</video>
<p style="color: gray;">Elegant, simple, chef's kiss</p>

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/VFX/HexPin.mp4" type="video/mp4">
</video>
<p style="color: gray;">I can do this all day... but I don't have to! It only takes about 15 minutes to configure one of these bad boys now.</p>

## Solution

> The tool I created is a **Unity amplify shader** VFX minikit combined with some 3d models.

Using photoshop to subdivide a circle into equidistant lines of equal lenght gave me an idea: what if I used Vertex Color on torusses to do exactly that?

So, combining multiple rudimentary shapes: Quads, Circles, Hexes, Squares and Triangles, we can quickly produce a variety of dynamic UI pins and gizmos. All using the same tool.

There's often quite a fuss over world-space UI elements, about whether or not to render them on top of the rest of the geometry. 
Depending on how crowded the visuals are, I tend to lean towards partial fading.

<img src="Projects/VFX/RenderOnTop.gif" alt="renderquirk" style="height: 280px; width: auto">  
<span style="color: gray;"></span>
