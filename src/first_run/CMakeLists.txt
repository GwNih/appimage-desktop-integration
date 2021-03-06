SET(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

find_package(Qt5 COMPONENTS Gui Widgets)

add_executable(appimage_first_run
    main.cpp
    $<TARGET_OBJECTS:appimage_dektop_integration>
    gui/ValidationDialog.h
    gui/ValidationDialog.cpp
    gui/ValidationDialog.ui
    gui/UiController.cpp
    gui/UiController.h
    gui/UnsecureAppimageDialog.h
    gui/UnsecureAppimageDialog.cpp
    gui/UnsecureAppimageDialog.ui
    gui/DeploymentDialog.h
    gui/DeploymentDialog.cpp
    gui/DeploymentDialog.ui
    ../../res/res.qrc)

target_include_directories(appimage_first_run PRIVATE
    PRIVATE ${CMAKE_SOURCE_DIR}/src/core
    ${libappimage_INCLUDE_DIRECTORIES}
    )

target_link_libraries(appimage_first_run libappimage Qt5::Core Qt5::Gui Qt5::Widgets)

add_dependencies(appimage_first_run libappimage)

install(TARGETS appimage_first_run RUNTIME DESTINATION bin COMPONENT first-run)
install(FILES org.appimage.first_run.desktop DESTINATION share/applications COMPONENT first-run)
