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
)

if (NOT(TARGET glfw_static))
  add_subdirectory(3rdParty/glfw)
endif()
target_link_libraries(owlViewer-config INTERFACE glfw_static)

if (NOT(TARGET stb_image))
  add_subdirectory(3rdParty/stb_image)
endif()
target_link_libraries(owlViewer-config INTERFACE stb_image)

add_subdirectory(owlViewer)
