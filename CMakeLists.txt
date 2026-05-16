cmake_minimum_required(VERSION 3.15)
project(cmd-model-target VERSION 0.1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if(NOT TARGET osk)
    find_package(osk 1.0.0 REQUIRED)
endif()

add_library(model_target STATIC src/target.cpp)
target_include_directories(model_target PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)
target_link_libraries(model_target PUBLIC osk)

install(TARGETS model_target EXPORT model_target-targets ARCHIVE DESTINATION lib)
install(FILES include/target.h           DESTINATION include)
install(FILES Config/default_params.yaml DESTINATION share/cmd-model-target)
