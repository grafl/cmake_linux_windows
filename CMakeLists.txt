cmake_minimum_required(VERSION 3.25)

project(ktb LANGUAGES CXX)

add_executable(ktb main.cpp)

find_package(wxWidgets COMPONENTS core base OPTIONAL_COMPONENTS net)
set(wxWidgets_CONFIG_OPTIONS --toolkit=base --prefix=/usr)

message("--------------------------------------------------------------------------------")
if(LINUX)
	# Linux
	message("Linux")
	include(${wxWidgets_USE_FILE})
	message("    wxWidgets_FOUND            : ${wxWidgets_FOUND}")
	message("    wxWidgets_INCLUDE_DIRS     : ${wxWidgets_INCLUDE_DIRS}")
	message("    wxWidgets_LIBRARIES        : ${wxWidgets_LIBRARIES}")
	message("    wxWidgets_LIBRARY_DIRS     : ${wxWidgets_LIBRARY_DIRS}")
	message("    wxWidgets_DEFINITIONS      : ${wxWidgets_DEFINITIONS}")
	message("    wxWidgets_DEFINITIONS_DEBUG: ${wxWidgets_DEFINITIONS_DEBUG}")
	message("    wxWidgets_USE_FILE         : ${wxWidgets_CXX_FLAGS}")
	message("    wxWidgets_CXX_FLAGS        : ${wxWidgets_USE_FILE}")
elseif(WIN32 OR MSVC OR MSYS OR MINGW)
	# Windows
	message("Windows")
	message("    wxWidgets_ROOT_DIR                : ${wxWidgets_ROOT_DIR}")
	message("    wxWidgets_LIB_DIR                 : ${wxWidgets_LIB_DIR}")
	message("    wxWidgets_CONFIGURATION           : ${wxWidgets_CONFIGURATION}")
	message("    wxWidgets_EXCLUDE_COMMON_LIBRARIES: ${wxWidgets_EXCLUDE_COMMON_LIBRARIES}")
else()
	# Apple
	message("APPLE")
endif()
message("--------------------------------------------------------------------------------")

if(wxWidgets_FOUND)
	target_link_libraries(ktb PRIVATE ${wxWidgets_LIBRARIES})
endif()
