# Copyright (c) 2015 - 2020 Advanced Micro Devices, Inc. All rights reserved.
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.  IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
# THE SOFTWARE.

cmake_minimum_required(VERSION 3.5)
project(nn_hip CXX)

set(NN_HIP_SOURCES
    nn_hip_kernels.cpp
    )

    set(hip_library_name amdhip64)
    set_source_files_properties(${NN_HIP_SOURCES} PROPERTIES HIP_SOURCE_PROPERTY_FORMAT 1)
    set(HIP_CXX_FLAGS -std=c++14)

    if(CMAKE_BUILD_TYPE MATCHES Debug)
        set(HIP_CXX_FLAGS ${HIP_CXX_FLAGS} -g)
    ENDIF()

    hip_add_library(nn_hip ${NN_HIP_SOURCES} HIPCC_OPTIONS "${HIP_CXX_FLAGS}" SHARED)
    target_compile_definitions(nn_hip PRIVATE __HIP_PLATFORM_HCC__)
    install(TARGETS nn_hip DESTINATION lib)

