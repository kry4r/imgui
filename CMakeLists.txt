add_library(imgui STATIC
    imgui.cpp
    imgui_tables.cpp
    imgui_draw.cpp
    imgui_widgets.cpp
    imgui_demo.cpp
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_vulkan.cpp
    backends/imgui_impl_glfw.h
    backends/imgui_impl_vulkan.h
)

target_include_directories(imgui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_include_directories(imgui PUBLIC
    ${Vulkan_INCLUDE_DIRS}
    ../glfw/include
)

target_link_libraries(imgui ${Vulkan_LIBRARIES} glfw)
