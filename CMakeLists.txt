cmake_minimum_required(VERSION 3.25)

project(ktb)

find_package(wxWidgets REQUIRED gl core base OPTIONAL_COMPONENTS net)
include(${wxWidgets_USE_FILE})

add_executable(ktb main.cpp)
target_link_libraries(wxTest PRIVATE ${wxWidgets_LIBRARIES})
