# ======================================================================== #
# Copyright 2018-2026 Ingo Wald                                            #
#                                                                          #
# Licensed under the Apache License, Version 2.0 (the "License");          #
# you may not use this file except in compliance with the License.         #
# You may obtain a copy of the License at                                  #
#                                                                          #
#     http://www.apache.org/licenses/LICENSE-2.0                           #
#                                                                          #
# Unless required by applicable law or agreed to in writing, software      #
# distributed under the License is distributed on an "AS IS" BASIS,        #
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. #
# See the License for the specific language governing permissions and      #
# limitations under the License.                                           #
# ======================================================================== #

set(OpenGL_GL_PREFERENCE "LEGACY")
find_package(OpenGL REQUIRED OPTIONAL_COMPONENTS OpenGL)

if (NOT (TARGET owl::owl))
  message(FATAL_ERROR "Your CMakefile needs to include OWL before including owlGLFWViewer")
endif()
  
add_library(owlGLFWViewer STATIC
  OWLViewer.h
  OWLViewer.cpp

  ColorMaps.h
  ColorMaps.cpp

  XFEditor.h
  XFEditor.cpp
  
  Camera.h 
  Camera.cpp
  
  InspectMode.h
  InspectMode.cpp
  
  FlyMode.h
  FlyMode.cpp

  ../3rdParty/imgui/imgui.cpp
  ../3rdParty/imgui/imgui_demo.cpp
  ../3rdParty/imgui/imgui_draw.cpp
  ../3rdParty/imgui/imgui_tables.cpp
  ../3rdParty/imgui/imgui_widgets.cpp
  ../3rdParty/imgui/backends/imgui_impl_glfw.cpp
  ../3rdParty/imgui/backends/imgui_impl_opengl3.cpp
)

if(TARGET OpenGL::OpenGL)
  target_link_libraries(owlGLFWViewer PUBLIC OpenGL::OpenGL)
else()
  target_link_libraries(owlGLFWViewer PUBLIC OpenGL::GL)
endif()

target_link_libraries(owlGLFWViewer
  PUBLIC
  owl::owl
  owlViewer-config
)

