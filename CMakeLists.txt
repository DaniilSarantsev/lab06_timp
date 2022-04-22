cmake_minimum_required(VERSION 3.11)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(CPACK_GENERATOR_DEB OFF)
option(CPACK_GENERATOR_RPM OFF)
option(CPACK_GENERATOR_MSI OFF)
option(CPACK_GENERATOR_DMG OFF)

project(solver)
set(PRINT_VERSION_MAJOR 0)
set(PRINT_VERSION_MINOR 1)
set(PRINT_VERSION_PATCH 0)
set(PRINT_VERSION_TWEAK 0)
set(PRINT_VERSION 
${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
set(PRINT_VERSION_STRING "v${PRINT_VERSION}")

add_executable(solver_app ${CMAKE_CURRENT_SOURCE_DIR}/solver_application/equation.cpp)

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib ${CMAKE_CURRENT_SOURCE_DIR}/solver_lib)

add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/formatter_ex_lib formatter_ex)
add_subdirectory(${CMAKE_CURRENT_SOURCE_DIR}/solver_lib solver_lib)

target_link_libraries(solver_app formatter_ex solver_lib)

install(TARGETS solver_app RUNTIME DESTINATION bin)

set(CPACK_SOURCE_GENERATOR "TGZ;ZIP")
if(CPACK_GENERATOR_RPM)
    set(CPACK_GENERATOR "RPM")
endif()
if(CPACK_GENERATOR_DEB)
    set(CPACK_DEBIAN_PACKAGE_MAINTAINER "DaniilSarantsev")
    set(CPACK_GENERATOR "DEB")
endif()
if(CPACK_GENERATOR_MSI)
    set(CPACK_GENERATOR "WIX")
endif()
if(CPACK_GENERATOR_DMG)
    set(MACOSX_BUNDLE TRUE)
    set(CPACK_GENERATOR "DragNDrop")
endif()

include(CPackConfig.cmake)








