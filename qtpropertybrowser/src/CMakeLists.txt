SET(KIT_SRCS
  qtbuttonpropertybrowser.cpp
  qteditorfactory.cpp
  qtgroupboxpropertybrowser.cpp
  qtpropertybrowser.cpp
  qtpropertybrowserutils.cpp
  qtpropertymanager.cpp
  qttreepropertybrowser.cpp
  qtvariantproperty.cpp
  )
  
SET(KIT_HEADERS
  qtbuttonpropertybrowser.h
  qteditorfactory.h
  qtgroupboxpropertybrowser.h
  qtpropertybrowser.h
  qtpropertybrowserutils_p.h
  qtpropertymanager.h
  qttreepropertybrowser.h
  qtvariantproperty.h
)
  
INCLUDE_DIRECTORIES(
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_BINARY_DIR}
  )

# init_qt: Let's do the CMake job for us
set(CMAKE_AUTOMOC ON) # For meta object compiler
set(CMAKE_AUTORCC ON) # Resource files
set(CMAKE_AUTOUIC ON) # UI files

if(NOT CMAKE_DEBUG_POSTFIX)
  set(CMAKE_DEBUG_POSTFIX d)
endif()

# build shared library if requested
IF (${PROJECT_NAME}_BUILD_SHARED_LIBS)
	ADD_LIBRARY(${PROJECT_NAME} SHARED
	  ${KIT_SRCS}
	  ${KIT_HEADERS}
	  )
ELSE()
ADD_LIBRARY(${PROJECT_NAME} STATIC
  ${KIT_SRCS}
  ${KIT_HEADERS}
  )
ENDIF()

TARGET_LINK_LIBRARIES(
  ${PROJECT_NAME}
  Qt5::Widgets
  Qt5::Core
  )

INSTALL(
  TARGETS ${PROJECT_NAME}
  DESTINATION bin #<-- set destination
)

INSTALL(
  FILES ${KIT_HEADERS}
  DESTINATION inc #<-- check destination
)