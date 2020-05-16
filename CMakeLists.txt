# 设置cmake版本
cmake_minimum_required(VERSION 3.0.0)

# 设置项目名称为dome 
# 这里对应变量${PROJECT_NAME}
project(dome VERSION 0.1.0)

# 设置引用目录 可省略头文件目录
include_directories(${PROJECT_SOURCE_DIR}/include/)

# 搜索src模板下的cpp文件（顶层）设置到变量SOURCE_FILES
file(GLOB_RECURSE SOURCE_FILES ${PROJECT_SOURCE_DIR}/src/*cpp)
# 打印
#message(${SOURCE_FILES})

# 这里设置两个库 dome_src dome_libsrc
# 这里有个奇异的点就是 库的名字必须是${PROJECT_NAME}这个开头 不然无法链接到
add_library(${PROJECT_NAME}_src SHARED ${SOURCE_FILES})
# 这个是直接输入源文件到库
add_library(${PROJECT_NAME}_libsrc SHARED libsrc/i.cpp)

# 添加可执行文件 编译
add_executable(${PROJECT_NAME} example/i_love_China.cpp)

# 这里把库文件链接到可执行文件中
target_link_libraries(${PROJECT_NAME}
${PROJECT_NAME}_src
${PROJECT_NAME}_libsrc
)

