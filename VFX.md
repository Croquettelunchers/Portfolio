[About Me](index.md) | [Projects](Projects.md) 

# VFX

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
