# CMakeList.txt : CMake project for CMakeProject3, include source and define
# project specific logic here.
#

# Add source to this project's executable.
add_executable (CMakeProject3 
"CMakeProject3.cpp" 
"CMakeProject3.h"
"Aircraft.cpp"
"Entity.cpp"
"Game.cpp"
"SceneNode.cpp"
"SpriteNode.cpp"
"World.cpp"
)

target_link_libraries(CMakeProject3 ${CMAKE_CURRENT_SOURCE_DIR}/lib/sfml-audio.lib)
target_link_libraries(CMakeProject3 ${CMAKE_CURRENT_SOURCE_DIR}/lib/sfml-graphics.lib)
target_link_libraries(CMakeProject3 ${CMAKE_CURRENT_SOURCE_DIR}/lib/sfml-network.lib)
target_link_libraries(CMakeProject3 ${CMAKE_CURRENT_SOURCE_DIR}/lib/sfml-system.lib)
target_link_libraries(CMakeProject3 ${CMAKE_CURRENT_SOURCE_DIR}/lib/sfml-window.lib)

set(FILES_TO_COPY
    ${CMAKE_CURRENT_SOURCE_DIR}/bin/sfml-audio-2.dll
    ${CMAKE_CURRENT_SOURCE_DIR}/bin/sfml-graphics-2.dll
    ${CMAKE_CURRENT_SOURCE_DIR}/bin/sfml-network-2.dll
    ${CMAKE_CURRENT_SOURCE_DIR}/bin/sfml-system-2.dll
    ${CMAKE_CURRENT_SOURCE_DIR}/bin/sfml-window-2.dll
)

foreach(file ${FILES_TO_COPY}) 
    add_custom_command(TARGET CMakeProject3 POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy
        ${file}  
        $<TARGET_FILE_DIR:CMakeProject3>  
    )
endforeach()

add_custom_command(TARGET CMakeProject3 POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory 
        ${CMAKE_CURRENT_SOURCE_DIR}/Media
        $<TARGET_FILE_DIR:CMakeProject3>/Media  
    )

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET CMakeProject3 PROPERTY CXX_STANDARD 20)
endif()

# TODO: Add tests and install targets if needed.
