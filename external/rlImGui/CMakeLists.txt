cmake_minimum_required(VERSION 3.12)

project(rllmGui)

add_library(rllmGui STATIC
	includes/rlImGui.h
	src/rllmGui.cpp
	
	includes/rllmGuiColors.h
	
	includes/imgui_impl_raylib.h
	
	#extras/FA6FreeSolidFontData.h
	#extras/IconsFontAwesome6.h
	
	#resources/driusstraight.ttf
)

target_include_directories(rllmGui PUBLIC includes)