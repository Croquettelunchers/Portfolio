[About Me](index.md) | [Projects](Projects.md) 

# Interior Lightbaking

I was given a few days to systemize and document interior lightbaking for real-time navigable environments. The following pictures are some of the shots from these experiments. 
The models were provided by my colleagues.

> Shot in **Unity**. Baked using [Bakery](https://assetstore.unity.com/packages/tools/level-design/bakery-gpu-lightmapper-122218)

This is my favorite shot of them all. It was taken for documentation purposes to outline how transparent objects (such as curtains) need special treatment; to be on their own layer.
<img src="Projects/Interiors/Interior1.png" style="height: auto; width: auto">  

Unity's HDR-compatible shader (also known as **Skybox material**) is extremely rudimentary. We needed to craft a more potent one. This is a lot more important than it seems for 2 reasons:  
1. Archviz's clients aren't just selling space. In most cases, they're selling *a view*.
2. HDRI have a huge impact on **ambiant lighting**.

We knew that clients would likely not provide proper HDRI or often stitched-up drone images instead. Therefore, we had to prepare for odd colorings, distortions, misorientations and off-positionning.  
<video controls width="560" style="display: block; margin: 0 auto;">
  <source src="Projects/Interiors/HDRI_Controller.mp4" type="video/mp4">
</video>

<img src="Projects/Interiors/Interior2.png" style="height: auto; width: auto">  

These apps doubled-down as interior design tools in which customers could pick and choose which finish to give to their countertops, cupboards etc.
Considering light bounces, all interchangeable assets had to be baked with neutral colors.

<span style="color: gray;">Note: non-physical trick lights could then be added to the mix to compensate, but we've never had to push it this far.</span>

<img src="Projects/Interiors/Interior4.png" style="height: auto; width: auto">   

Caustics from the glass were only 2 quads with chromatic aberation surface shaders. Decals were not featured in the engine at the time.

<img src="Projects/Interiors/Interior5.png" style="height: auto; width: auto">  
Different styling, same kitchen. 

<img src="Projects/Interiors/Interior7.png" style="height: auto; width: auto">  



