cmake_minimum_required(VERSION 3.18)
project("constexprhash" VERSION 0.1.0 LANGUAGES CXX)

add_library(constexprhash INTERFACE)
target_include_directories(constexprhash INTERFACE 
	$<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
    $<INSTALL_INTERFACE:include>
)
target_compile_features(constexprhash INTERFACE cxx_std_23)
set_target_properties(constexprhash PROPERTIES
	CXX_STANDARD 23
	CXX_STANDARD_REQUIRED ON
	CXX_EXTENSIONS OFF
)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${PROJECT_BINARY_DIR}/constexprhashConfigVersion.cmake"
    VERSION 0.1
    COMPATIBILITY AnyNewerVersion
)

install(TARGETS constexprhash
    EXPORT constexprhashTargets
    LIBRARY DESTINATION lib COMPONENT Runtime
    ARCHIVE DESTINATION lib COMPONENT Development
    RUNTIME DESTINATION bin COMPONENT Runtime
    PUBLIC_HEADER DESTINATION include COMPONENT Development
    BUNDLE DESTINATION bin COMPONENT Runtime
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
    "${PROJECT_SOURCE_DIR}/cmake/constexprhashConfig.cmake.in"
    "${PROJECT_BINARY_DIR}/constexprhashConfig.cmake"
    INSTALL_DESTINATION lib/cmake/constexprhash
)

install(EXPORT constexprhashTargets DESTINATION lib/cmake/constexprhash)
install(FILES "${PROJECT_BINARY_DIR}/constexprhashConfigVersion.cmake"
              "${PROJECT_BINARY_DIR}/constexprhashConfig.cmake"
        DESTINATION lib/cmake/constexprhash)
install(DIRECTORY ${PROJECT_SOURCE_DIR}/include/ DESTINATION include)


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