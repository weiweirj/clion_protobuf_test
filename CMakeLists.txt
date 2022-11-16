cmake_minimum_required(VERSION 3.22)
project(untitled4)


# Find required protobuf package
find_package(Protobuf REQUIRED)
if (PROTOBUF_FOUND)
    message(STATUS "protobuf library found")
else ()
    message(FATAL_ERROR "protobuf library is needed but cant be found")
endif ()


set(CMAKE_CXX_STANDARD 23)


include_directories(${PROTOBUF_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_BINARY_DIR})
protobuf_generate_cpp(PROTO_SRCS PROTO_HDRS addressbook.proto)
message(${PROTO_SRCS} ${PROTO_HDRS})


add_executable(untitled4 main.cpp ${PROTO_SRCS} ${PROTO_HDRS})

target_include_directories(untitled4
        PUBLIC
        ${PROTOBUF_INCLUDE_DIRS}
        ${CMAKE_CURRENT_BINARY_DIR}
        )
# link the exe against the libraries
target_link_libraries(untitled4
        ${PROTOBUF_LIBRARIES}
        )