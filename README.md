# owl-project/glfwViewer - A 3D interactive viewer base class based on GLFW.

This repo provides a base class `OWLViewer` that can be used to build
interactive 3D model viewers; primarily for OWL/OptiX.

OWLViewer managed window creation, camera motion, displaying of
frames, etc, and allows the user to subclass and override functions
like `renderFrame()` to do the actual rendering.
