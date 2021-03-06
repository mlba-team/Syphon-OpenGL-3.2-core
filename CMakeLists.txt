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

target_include_directories( Syphon
    PUBLIC "${CMAKE_CURRENT_LIST_DIR}/include"
)

set_target_properties( Syphon PROPERTIES
    FRAMEWORK TRUE
    MACOSX_FRAMEWORK_IDENTIFIER "info.v002.Syphon"
    MACOSX_FRAMEWORK_SHORT_VERSION_STRING "0.0.2"
    MACOSX_FRAMEWORK_BUNDLE_VERSION "insidMWM/Syphon-OpenGL-3.2-core"
    PUBLIC_HEADER "${HEADER}"
)
mz_target_props(Syphon)
