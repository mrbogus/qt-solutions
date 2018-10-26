
SET(example_name canvas_variant)

SET(KIT_SRCS
  main.cpp
  mainwindow.cpp
  mainwindow.h
  qtcanvas.cpp
  qtcanvas.h
  )
  
INCLUDE_DIRECTORIES(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_BINARY_DIR}
  )

# init_qt: Let's do the CMake job for us
set(CMAKE_AUTOMOC ON) # For meta object compiler
  
ADD_EXECUTABLE(${example_name} ${KIT_SRCS})
TARGET_LINK_LIBRARIES(${example_name} ${PROJECT_NAME} Qt5::Widgets)
