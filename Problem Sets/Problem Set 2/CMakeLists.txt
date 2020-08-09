############################################################################
# <summary> CMakeLists.txt for OpenCV and CUDA. </summary>
# <date>    2012-02-07          </date>
# <author>  Quan Tran Minh. edit by Johannes Kast, Michael Sarahan </author>
# <email>   quantm@unist.ac.kr  kast.jo@googlemail.com msarahan@gmail.com</email>
############################################################################
cmake_minimum_required (VERSION 3.5)
project(problem_set_2)

set (CMAKE_CXX_FLAGS "-std=c++14 -fPIC")

# Opencv
find_package(OpenCV REQUIRED)
message(STATUS "OPENCV_INCLUDE_DIRS" ${OppenCV_INCLUDE_DIRS})

# find cuda
find_package(CUDA REQUIRED)
include_directories (${CUDA_INCLUDE_DIRS})
message (STATUS "CUDA_INCLUDE_DIRS: ${CUDA_INCLUDE_DIRS}")
link_directories(${CUDA_TOOLKIT_ROOT_DIR}/lib64/)

# collect source files

file( GLOB  hdr *.hpp *.h )
file( GLOB  cu  *.cu)
SET (HW2_files main.cpp reference_calc.cpp compare.cpp)
    
CUDA_ADD_EXECUTABLE(HW2 ${HW2_files} ${hdr} ${cu})
target_link_libraries(HW2 ${OpenCV_LIBS})