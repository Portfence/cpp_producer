# ## 'test' directory is a standalone project

cmake_minimum_required(VERSION 3.16.3 FATAL_ERROR)

project(producer_test CXX)

# For finding dependencies with Conan Package Manager
set(CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR} ${CMAKE_MODULE_PATH})
set(CMAKE_PREFIX_PATH ${CMAKE_BINARY_DIR} ${CMAKE_PREFIX_PATH})

include(CTest)

find_package(doctest CONFIG REQUIRED)
find_package(trompeloeil CONFIG REQUIRED)
if (NOT TARGET producer::producer)
    find_package(producer CONFIG REQUIRED)
endif()

add_executable(${PROJECT_NAME}
    test_main.cpp
    test_source_a.cpp
)

target_link_libraries(${PROJECT_NAME}
    PRIVATE
        producer::producer
        doctest::doctest
        trompeloeil::trompeloeil
)

add_test(NAME producer.unit_tests COMMAND ${PROJECT_NAME})
