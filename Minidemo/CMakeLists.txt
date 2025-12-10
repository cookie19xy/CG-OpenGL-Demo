cmake_minimum_required(VERSION 3.20)
project(MiniEngineDemo)

# 设置C++标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 查找vcpkg安装的库
find_package(glfw3 CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)

# 包含头文件目录
include_directories(${CMAKE_SOURCE_DIR}/src)

# 源文件列表
file(GLOB SOURCES 
    ${CMAKE_SOURCE_DIR}/src/*.cpp
    ${CMAKE_SOURCE_DIR}/src/*.c
)

# 生成可执行文件
add_executable(${PROJECT_NAME} ${SOURCES})

# 链接库
target_link_libraries(${PROJECT_NAME} PRIVATE 
    glfw 
    glm::glm 
    opengl32  # Windows OpenGL库
)

# 复制shaders目录到构建目录
add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
    ${CMAKE_SOURCE_DIR}/shaders
    $<TARGET_FILE_DIR:${PROJECT_NAME}>/shaders
)