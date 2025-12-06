cmake_minimum_required(VERSION 3.16)

project(Settings-Customer LANGUAGES CXX)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Gui LinguistTools)
find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Gui LinguistTools)

set(TS_FILES Settings-Customer_en_US.ts)

add_library(Settings-Customer SHARED
  Settings-Customer_global.h
  settingscustomer.cpp
  settingscustomer.h
  ${TS_FILES}
)

target_link_libraries(Settings-Customer PRIVATE Qt${QT_VERSION_MAJOR}::Gui)

target_compile_definitions(Settings-Customer PRIVATE SETTINGS_CUSTOMER_LIBRARY)

if(COMMAND qt_create_translation)
    qt_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})
else()
    qt5_create_translation(QM_FILES ${CMAKE_SOURCE_DIR} ${TS_FILES})
endif()
add_subdirectory(libs/yaml-cpp)
