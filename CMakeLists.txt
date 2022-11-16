cmake_minimum_required(VERSION 3.18)
project("constexprhash" VERSION 0.1.0 LANGUAGES CXX)

add_library(constexprhash INTERFACE)
target_include_directories(constexprhash INTERFACE src/)
set_target_properties(constexprhash PROPERTIES
	CXX_STANDARD 23
	CXX_STANDARD_REQUIRED ON
	CXX_EXTENSIONS OFF
)

if(CMAKE_TESTING_ENABLED)
	find_package(GTest REQUIRED)
	add_executable(test_constexprhash test/test_cityhash.cpp)
	target_link_libraries(test_constexprhash PRIVATE GTest::GTest GTest::Main constexprhash)
	set_target_properties(test_constexprhash PROPERTIES
		CXX_STANDARD 23
		CXX_STANDARD_REQUIRED ON
		CXX_EXTENSIONS OFF
	)

	gtest_discover_tests(test_constexprhash)
endif()