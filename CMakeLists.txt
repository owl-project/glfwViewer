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

cmake_minimum_required(VERSION 3.24)

project(OWL_GLFWViewer)

add_library(owlViewer-config INTERFACE)
target_include_directories(owlViewer-config INTERFACE
  ${CMAKE_CURRENT_LIST_DIR}
  ${CMAKE_CURRENT_LIST_DIR}/3rdParty/imgui
  ${CMAKE_CURRENT_LIST_DIR}/3rdParty/imgui/backends
)

find_package(glfw3 3.3)
if (NOT(TARGET glfw))
  add_subdirectory(3rdParty/glfw)
endif()
target_link_libraries(owlViewer-config INTERFACE glfw)
#target_link_libraries(owlViewer-config INTERFACE glfw_static)

if (NOT(TARGET stb_image))
  add_subdirectory(3rdParty/stb_image)
endif()
target_link_libraries(owlViewer-config INTERFACE stb_image)

set(OpenGL_GL_PREFERENCE "LEGACY")
find_package(OpenGL REQUIRED OPTIONAL_COMPONENTS OpenGL)

if (NOT (TARGET owl::owl))
  message(FATAL_ERROR "Your CMakefile needs to include OWL before including owlGLFWViewer")
endif()
  
add_library(owlGLFWViewer STATIC
  
  owlViewer/OWLViewer.h
  owlViewer/OWLViewer.cpp

  owlViewer/ColorMaps.h
  owlViewer/ColorMaps.cpp

  owlViewer/XFEditor.h
  owlViewer/XFEditor.cpp
  
  owlViewer/Camera.h 
  owlViewer/Camera.cpp
  
  owlViewer/InspectMode.h
  owlViewer/InspectMode.cpp
  
  owlViewer/FlyMode.h
  owlViewer/FlyMode.cpp

  3rdParty/imgui/imgui.cpp
  3rdParty/imgui/imgui_demo.cpp
  3rdParty/imgui/imgui_draw.cpp
  3rdParty/imgui/imgui_tables.cpp
  3rdParty/imgui/imgui_widgets.cpp
  3rdParty/imgui/backends/imgui_impl_glfw.cpp
  3rdParty/imgui/backends/imgui_impl_opengl3.cpp
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

