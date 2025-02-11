[About Me](index.md) | [Projects](Projects.md) 

# Tremblant Winter-Shading

For this project my task was to convert an entire existing project to a winter environment. 

>This is a **Unity real-time Archviz** simulation.

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/Tremblant/PortfolioTremblant.mp4" type="video/mp4">
</video>

## Solution

Here was my approach:  
- Introduce a single new **Global shader property**.  
- Operate at **surface shading** level.  
- All the project's shaders structure follow this pattern:  
<img src="Projects/Tremblant/StructureofSnowup.PNG" alt="Structure" style="height: auto; width: auto">  

A snow particles's spawner forms a box around the camera, just big enough that if you move the camera around we don't lose the effect. It's nothing fancy. Performances were good enough that we could enable collisions, letting them stick around a little bit on surfaces before fading away.  

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/Tremblant/PortfolioTremblant2.mp4" type="video/mp4">
</video>

## Location Accurate Environment

These are the actual sunsets and sunrise positions for both summer and winter at this location, somewhere on Mont Tremblant.  

Sky colors as well as sunset and sunrise positions were adapted to the reduced daytime that happens during Quebec winters.  
<span style="color: gray;">I was involved in design and planning for this feature. Coding was done by other colleagues. I did configure the results.</span>

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/Tremblant/PortfolioTremblant3.mp4" type="video/mp4">
</video>
<p style="color: gray;">This is one of the rare times I've worked with someone else on lighting on a project. I think we did good!</p>   

## Sample Prototype Snow

Notice in the following video how some surfaces get disconnected (right above the gizmo's green arrow) from the rest of the object while the displacement occurs. This is because assets need to be prepared with contiguous normals (or a proxy map of this) in order for snow accumulation to reach its full potential.  

<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/Tremblant/Snow.mp4" type="video/mp4">
</video>
<span style="color: gray;">Proto-Snow: Version not final</span>  

