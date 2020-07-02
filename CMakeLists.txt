cmake_minimum_required(VERSION 3.0.0)
project(mkfatfs VERSION 0.1.0)

# # specify the C++ standard
# set(CMAKE_CXX_STANDARD 11)
# set(CMAKE_CXX_STANDARD_REQUIRED True)

configure_file(Config.h.in Config.h)

include(CTest)
enable_testing()

include_directories(.)
include_directories(esp_idf/include)
include_directories(esp_idf/freertos/include)
include_directories(filesystem/diskio/include)
include_directories(filesystem/fatfs/include)
include_directories(filesystem/vfs/include)
include_directories(tclap)

add_subdirectory(esp_idf)
add_subdirectory(filesystem/diskio)
add_subdirectory(filesystem/fatfs)
add_subdirectory(filesystem/vfs)
add_subdirectory(esp_idf/freertos)

# aux_source_directory(esp_idf DIR_ESP_IDF)
# aux_source_directory(esp_idf/freertos DIR_RTOS)
# aux_source_directory(filesystem/diskio DIR_DISKIO)
# aux_source_directory(filesystem/fatfs DIR_FATFS)
# aux_source_directory(filesystem/vfs DIR_VFS)

# add_executable(mkfatfs ${DIR_SRCS} ${DIR_ESP_IDF} ${DIR_RTOS} ${DIR_DISKIO} ${DIR_FATFS} ${DIR_VFS})
if (WIN32)
    add_executable(mkfatfs main.cpp pack_win32.cpp)
elseif(APPLE) 
	MESSAGE(STATUS "Now is Apple systens.")
elseif(UNIX)
    add_executable(mkfatfs main.cpp pack_linux.cpp)
endif() 

target_link_libraries(mkfatfs -Wl,--start-group esp-idf vfs diskio fatfs freertos -Wl,--end-group)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)

target_include_directories(mkfatfs PUBLIC
                           "${PROJECT_BINARY_DIR}"
                           )