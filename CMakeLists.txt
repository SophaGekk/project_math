cmake_minimum_required(VERSION 3.21)
project(pop VERSION 0.0.1 LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 2.6.x)
FetchContent_MakeAvailable(SFML)

add_executable(pop 3Dengine.cpp cell.cpp fileio.cpp)

add_custom_command(TARGET pop POST_BUILD
                   
                   COMMAND ${CMAKE_COMMAND}
                   ARGS -E copy_directory
                        ${PROJECT_SOURCE_DIR}/resources
                        $<TARGET_FILE_DIR:pop>/resources
                   VERBATIM)

target_link_libraries(pop PRIVATE sfml-graphics sfml-system sfml-window sfml-audio )

target_compile_features(pop PRIVATE cxx_std_14)