#
# CMakeLists.txt
#
# Copyright (c) 2015 MLBA-Team
# All rights reserved.
#
# @LICENSE_HEADER_START@
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
# * Redistributions of source code must retain the above copyright
#   notice, this list of conditions and the following disclaimer.
#
# * Redistributions in binary form must reproduce the above copyright
#   notice, this list of conditions and the following disclaimer in the
#   documentation and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
# ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
# WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
# DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDERS BE LIABLE FOR ANY
# DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
# (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
# LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
# ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
# SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# @LICENSE_HEADER_END@
#

file(GLOB SRC src/*.c src/*.m)
file(GLOB HEADER include/*.h)

mz_use_default_compiler_settings()

# assume an installation
include_directories(
    include
)

source_group(src FILES ${SRC})
source_group(includes FILES ${HEADER})

find_library(FOUNDATION Foundation REQUIRED)
find_library(OPENGL OpenGL REQUIRED)
find_library(COCOA Cocoa REQUIRED)
find_library(IOSURFACE IOSurface REQUIRED)
add_library(Syphon SHARED ${SRC} ${HEADER})
target_link_libraries(Syphon
    ${FOUNDATION}
    ${OPENGL}
    ${IOSURFACE}
    ${COCOA}
)

mz_target_props(Syphon)
set_target_properties( Syphon PROPERTIES
    INTERFACE_INCLUDE_DIRECTORIES "${CMAKE_CURRENT_LIST_DIR}/include"
)

set_property(TARGET Syphon PROPERTY FRAMEWORK TRUE)
set_property(TARGET Syphon PROPERTY PUBLIC_HEADER ${HEADER})
