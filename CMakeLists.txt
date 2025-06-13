cmake_minimum_required(VERSION 3.16)

project(imgui)

# ImGui source files
set(IMGUI_SOURCES
    imgui.cpp
    imgui_demo.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_vulkan.cpp
)

# ImGui header files
set(IMGUI_HEADERS
    imgui.h
    imgui_internal.h
    imconfig.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
    backends/imgui_impl_glfw.h
    backends/imgui_impl_vulkan.h
)

# Create imgui library
add_library(imgui STATIC ${IMGUI_SOURCES} ${IMGUI_HEADERS})

# Find required dependencies
find_package(Vulkan REQUIRED)
find_package(glfw3 REQUIRED)

# Set include directories
target_include_directories(imgui PUBLIC
    ${CMAKE_CURRENT_SOURCE_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

# Link libraries
target_link_libraries(imgui PUBLIC
    ${Vulkan_LIBRARIES}
    glfw
)

# Set target include directories for Vulkan
target_include_directories(imgui PUBLIC ${Vulkan_INCLUDE_DIRS})

# Platform-specific definitions
if(APPLE)
    target_compile_definitions(imgui PUBLIC VK_USE_PLATFORM_MACOS_MVK)
elseif(WIN32)
    target_compile_definitions(imgui PUBLIC VK_USE_PLATFORM_WIN32_KHR)
elseif(UNIX)
    target_compile_definitions(imgui PUBLIC VK_USE_PLATFORM_XLIB_KHR)
endif()

# Set target properties
set_target_properties(imgui PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON
)

# Export for parent scope
set(IMGUI_LIBRARIES imgui PARENT_SCOPE)
set(IMGUI_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR} PARENT_SCOPE)
