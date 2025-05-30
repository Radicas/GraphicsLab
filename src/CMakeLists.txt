# 收集源文件
file(GLOB_RECURSE SOURCES
        ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp
        ${SOURCES_PATH}/*.cpp
        ${SOURCES_PATH}/*.c
)

# 添加头文件目录
include_directories(
        ${HEADERS_PATH}
)

# 编译成库
add_executable(${PROJECT_NAME}
        ${SOURCES}
)

# 查找 OpenGL 和 GLEW
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(GLFW3 REQUIRED)


# 链接 OpenGL, GLEW 和 GLFW 库
target_link_libraries(${PROJECT_NAME} PRIVATE
        OpenGL::GL
        GLEW::GLEW
        glfw
        redcgl
)

if(UNIX)
        target_link_libraries(${PROJECT_NAME} PRIVATE
                m
        )
endif()

# 安装目标文件
install(TARGETS ${PROJECT_NAME}
        RUNTIME DESTINATION ${INSTALL_PATH}/bin
        LIBRARY DESTINATION ${INSTALL_PATH}/bin
        ARCHIVE DESTINATION ${INSTALL_PATH}/bin
)
