add_library(imgui STATIC 
    imgui.cpp
    imgui_tables.cpp
    imgui_draw.cpp
    imgui_widgets.cpp
    imgui_demo.cpp
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_vulkan.cpp
)
