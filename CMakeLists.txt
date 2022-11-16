cmake_minimum_required(VERSION 3.18)
project("constexpr-cityhash" VERSION 0.1.0 LANGUAGES CXX)

add_library(cityhash INTERFACE src/cityhash.hpp)
set_target_properties(cityhash PROPERTIES
	CXX_STANDARD 20
	CXX_STANDARD_REQUIRED ON
	CXX_EXTENSIONS OFF
)