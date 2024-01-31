cmake_minimum_required(VERSION 3.25)

project(ktb LANGUAGES CXX)

find_package(wxWidgets REQUIRED core base OPTIONAL_COMPONENTS net)

set(BUNDLE "")

# Get the latest abbreviated commit hash of the working branch
execute_process(
	COMMAND git log -1 --format=%h
	WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
	OUTPUT_VARIABLE GIT_HASH
	OUTPUT_STRIP_TRAILING_WHITESPACE
)
message("")
message("GIT_HASH: ${GIT_HASH}")
message("")

# file(TOUCH "${CMAKE_SOURCE_DIR}/git_version.h")
file(WRITE "${CMAKE_SOURCE_DIR}/git_version.h" "#ifndef GIT_VERSION_H\n")
file(APPEND "${CMAKE_SOURCE_DIR}/git_version.h" "#define GIT_VERSION_H\n")
file(APPEND "${CMAKE_SOURCE_DIR}/git_version.h" "\n")
file(APPEND "${CMAKE_SOURCE_DIR}/git_version.h" "extern const char *kGitHash = \"${GIT_HASH}\";\n")
file(APPEND "${CMAKE_SOURCE_DIR}/git_version.h" "\n")
file(APPEND "${CMAKE_SOURCE_DIR}/git_version.h" "#endif // GIT_VERSION_H\n")

if(wxWidgets_FOUND)
	if(LINUX)
		set(BUNDLE "")
		include(${wxWidgets_USE_FILE})
	elseif(WIN32 OR MSVC OR MSYS OR MINGW)
		set(BUNDLE "WIN32")
		if(wxWidgets_USE_FILE)
			include(${wxWidgets_USE_FILE})
		endif()
	else()
		set(BUNDLE "MACOSX_BUNDLE")
	endif()
	add_executable(${PROJECT_NAME} ${BUNDLE} main.cpp)
	target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_SOURCE_DIR})
	target_link_libraries(${PROJECT_NAME} PRIVATE ${wxWidgets_LIBRARIES})
else()
	message("No wxWidgets distribution found.")
endif()
