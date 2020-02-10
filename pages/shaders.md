# Stage 3 Graphics for Games: Hardware Shaders

## Video 
<iframe width="560" height="315" src="https://www.youtube.com/embed/DMzknMpKNUY" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

## Introduction
In this project I made use of OpenGL and shader language GLSL to build a series of shaders for application to a spinning cube. Vertex, fragment, geometry and tesselation shaders were implemented by themselves or in combinations with other shaders.

## What Was Learned
This was my first experience of programming my own shaders, so naturally I learned about the use of vertex, fragment, geometry and tesselation shaders. I also saw how textures could be used to generate variable heightmaps. 

## Implementation
Seven different shaders were implemented: 
1. A vertex shader to reduce the size of the cube over time by scaling down, giving the cube the appearance of shrinking into nothingness.
2. A fragment shader to blend the wooden cube texture into a 'worn down' appearance. 
3. A fragment shader to gradually reduce the opacity of the cube to fade into nothingness by reducing the alpha value over time. 
4. A geometry shader to form 8 smaller cubes from each vertex on the original cube which spread out and shrink, giving the image of the cube falling apart. 
5. A combination of a tesselation shader and geometry shader. The tesselation shader tesselates the cube and adjusts the height of the new vertices based on the texture to look stressed. The geometry shader then processes each tesselated triangle and pushes them along a normal to splinter the cube. A log curve is used to first 'hold' the splint image before pushing the fragments away.
6. A tesselation shader which uses a secondary texture as a heightmap to indent the cube and make a crater to a set depth over time. Phong lighting is used to highlight the shape of the crater. 
7. A tesselation shader to extend the surface of all cube faces with a heightmap based on the texture. Phong lighting is attached to the mouse which can be moved as a 'flashlight' to highlight the added depth in different ways.

## Possible Improvements
Some memory optimising could be completed by further removal of fragments from processing after a certain point, for example the deletion of the splinter fragments from shader 5 at a certain distance from the starting point. 
