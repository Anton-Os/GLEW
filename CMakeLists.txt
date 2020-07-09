cmake_minimum_required(VERSION 3.6)
project(GLEW DESCRIPTION "Personalized GLEW distro")

add_library(GLEW_lib
    STATIC
    glew.c
)

target_include_directories(
    GLEW_lib 
    PRIVATE ${CMAKE_SOURCE_DIR}
)

target_include_directories(GLEW_lib
	INTERFACE
	$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}>
	$<INSTALL_INTERFACE:include>
)

install(TARGETS GLEW_lib
	EXPORT GLEW
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
	FRAMEWORK DESTINATION lib
)

install(FILES
    ${CMAKE_SOURCE_DIR}/GL/eglew.h
    ${CMAKE_SOURCE_DIR}/GL/glew.h
    ${CMAKE_SOURCE_DIR}/GL/glxew.h
    ${CMAKE_SOURCE_DIR}/GL/wglew.h
    DESTINATION include/GL
)

install(EXPORT GLEW DESTINATION lib/GLEW FILE GLEW-config.cmake)