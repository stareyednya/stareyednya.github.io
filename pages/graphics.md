# Stage 4 Advanced Graphics for Games

## Result
Enable captions for descriptions of each feature as they are shown.
<iframe width="560" height="315" src="https://www.youtube.com/embed/VRl7ds2qX6Q" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

'A well thought out, technically excellent scene with a wide range of engineering features.' - Dr Rich Davision 

[View on Github](https://github.com/eleanoot/public-examples)

## Introduction
The brief for this project was to use OpenGL within Newcastle University's graphics framework NCLGL to render the scene of a landscape which changed over time. I interpreted this by having a camera move through a landscape that rose from the water, the movement triggering changes such as trees growing and snow beginning to fall.

## What Was Learned
This was my first large project with OpenGL and included features covered many techniques that made use of additional rendering aspects such as the depth buffer that I hadn't covered previously, for example in shadow mapping and post processing effects. In previous graphics projects I also had not previously used scene graphs for efficient rendering, so this project really got me to think about how to structure graphical scenes in the best way possible. 

## Implementation
My finished landscape scene contained a number of graphical features, both rendered on the screen and within the code for more efficient rendering:

* A __heightmap__ generated using an image and index buffering, which rises to its full height over time by use of a vertex shader. 
* Two textures used to cover the landscape of grass and rock, with each fragment being a mix of the two based on the gradient of that fragment's normal. This allowed for steeper surfaces to be textured as cliffs and everywhere else grass. __Triplanar texturing__ was used to prevent the steeper textures being stretched, and each texture was __normal mapped__ for extra detail.
* Rolling water waves created by __tessellation__, with shaders referencing the heightmap to only calculate fragments for darker portions of the map where water could be seen to __save on unnecessary tessellation__. 
* A full __environment skybox reflected__ in the water.
* __Scene graphs__: tree with leaves attached to a trunk grow into the scene. The full scene is also controlled by a scene graph, with each node able to contain its own shader and light to switch between during node drawing, and specialised nodes that can send extra uniforms to these shaders (such as the height modifier for the terrain). __Frustrum culling__ occurs based on the parent node to test for all of its children, of which the tree trunks might have many.
* __Shadow mapping__: the landscape and the character in the centre of the map cast shadows across the scene. The character moves with skeletal animation and its shadow updates with it. 
* __Skeletal animation__ was done on the GPU with hardware skinning, which would have allowed for more characters to be in the scene. 
* __Particle system:__ snow falls and gradually mixes the terrain with a snow colour over time. The particle system is __efficient in reusing particles__ once they come to the end of their life and have fallen onto the terrain rather than constantly emitting new objects.
* __Post processing effects__:
- A Gaussian blur.
- Edge detection using a Sobel filter.
- Colour grading using a redder colour table to brighten up the scene as though on a sunnier day. 
- The beginnings of a lens flare with streaks and intensity the more the scene light is being faced. 
- Split screen to show four different points of interest in the scene simultaneously. 

## Possible Improvements
A number of features such as shadow mapping, skybox reflections and the particle faces only take into account one direction, meaning the shown image may not always be accurate from certain angles. A good way to improve the scene to a more realistic standard would be the inclusion of multiple angles for mapping, and particle billboarding so the snow could always be seen. 

I would have also liked to show off the inclusion of multiple lights and their calculations in the scene, which could have been done via deferred rendering for further efficiency. 

