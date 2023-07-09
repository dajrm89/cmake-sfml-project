cmake_minimum_required(VERSION 3.21)
project(Timber LANGUAGES CXX)

include(FetchContent)
FetchContent_Declare(SFML
    GIT_REPOSITORY https://github.com/SFML/SFML.git
    GIT_TAG 2.6.x)
FetchContent_MakeAvailable(SFML)

add_executable(Timber src/main.cpp)
target_link_libraries(Timber PRIVATE sfml-graphics)
target_compile_features(Timber PRIVATE cxx_std_17)
if (WIN32 AND BUILD_SHARED_LIBS)
    add_custom_command(TARGET Timber POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy $<TARGET_RUNTIME_DLLS:Timber> $<TARGET_FILE_DIR:Timber> COMMAND_EXPAND_LISTS)
endif()

install(TARGETS Timber)
