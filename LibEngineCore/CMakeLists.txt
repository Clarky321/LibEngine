cmake_minimum_required(VERSION 3.12)

set(ENGINE_PROJECT_NAME LibEngineCore)

set(ENGINE_PUBLIC_INCLUDES
	includes/LibEngineCore/test.h
)

set(ENGINE_PRIVATE_SOURCES
	src/LibEngineCore/test.cpp
)

set(ENGINE_ALL_SOURCE
	${ENGINE_PUBLIC_INCLUDES}
	${ENGINE_PRIVATE_SOURCES}
)

add_library(${ENGINE_PROJECT_NAME} STATIC ${ENGINE_ALL_SOURCE})

source_group(TREE ${CMAKE_CURRENT_SOURCE_DIR} FILES ${ENGINE_ALL_SOURCE})

target_include_directories(${ENGINE_PROJECT_NAME}
	PUBLIC
		includes
	PRIVATE
		src
)

target_compile_features(${ENGINE_PROJECT_NAME} PUBLIC cxx_std_17)

# ------------------------------------------------------------------------------------- #

add_subdirectory(../external/raylib ${CMAKE_CURRENT_BINARY_DIR}/raylib)
target_link_libraries(${ENGINE_PROJECT_NAME} PUBLIC raylib)

# ------------------------------------------------------------------------------------- #

#add_subdirectory(../external/cmake-imgui ${CMAKE_CURRENT_BINARY_DIR}/cmake-imgui)
#target_link_libraries(${ENGINE_PROJECT_NAME} PUBLIC ImGui::imgui)

# ------------------------------------------------------------------------------------- #

#add_subdirectory(../external/rlImGui ${CMAKE_CURRENT_BINARY_DIR}/rlImGui)
#target_link_libraries(${ENGINE_PROJECT_NAME} PUBLIC rlImGui)

# ------------------------------------------------------------------------------------- #

set(IMGUI_INCLUDES
	../external/rlImGui/includes/rlImGui.h
	../external/rlImGui/includes/rlImGuiColors.h
	../external/rlImGui/includes/imgui_impl_raylib.h
	
	../external/rlImGui/extras/IconsFontAwesome6.h
	../external/rlImGui/extras/FA6FreeSolidFontData.h
)

set(IMGUI_SOURCES
	../external/rlImGui/src/rlImGui.cpp
)

add_library(rlImGui STATIC
	${IMGUI_INCLUDES}
	${IMGUI_SOURCES}
)

target_include_directories(rlImGui PUBLIC ../external/rlImGui)
target_link_libraries(${ENGINE_PROJECT_NAME} PUBLIC rlImGui)

# ------------------------------------------------------------------------------------- #

set(IMGUI_INCLUDES

	../external/imgui/imgui.h
	#../external/imgui/backends/imgui_impl_glfw.h
	../external/imgui/backends/imgui_impl_opengl3.h
)

set(IMGUI_SOURCES
	../external/imgui/imgui.cpp
	#../external/imgui/backends/imgui_impl_glfw.cpp
	../external/imgui/backends/imgui_impl_opengl3.cpp
	
	../external/imgui/imgui_draw.cpp
	../external/imgui/imgui_widgets.cpp
	../external/imgui/imgui_tables.cpp
	
	../external/imgui/imgui_demo.cpp
)

add_library(ImGui STATIC
	${IMGUI_INCLUDES}
	${IMGUI_SOURCES}
)

#target_include_directories(ImGui PUBLIC ../external)
target_include_directories(ImGui PUBLIC ../external/imgui)
#target_link_libraries(ImGui PRIVATE glad glfw)

#target_link_libraries(${ENGINE_PROJECT_NAME} PRIVATE ImGui)
target_link_libraries(${ENGINE_PROJECT_NAME} PUBLIC ImGui)
