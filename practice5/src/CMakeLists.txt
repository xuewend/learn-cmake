ADD_EXECUTABLE(curltest main.c)

FIND_PACKAGE(CURL)
IF(CURL_FOUND)
	MESSAGE(STATUS "CURL library found")
	INCLUDE_DIRECTORIES(/usr/include)
	TARGET_LINK_LIBRARIES(curltest libcurl.so)
	
ELSE(CURL_FOUND)
	MESSAGE(FATAL_ERROR "CURL library not found")
ENDIF(CURL_FOUND)

SET(mySources viewer.c)
SET(optionalSources)
SET(optionalLibs)

FIND_PACKAGE(JPEG)
IF(JPEG_FOUND)
	SET(optionalSources ${optionalSources} jpegview.c)
	INCLUDE_DIRECTORIES( ${JPEG_INCLUDE_DIR} )
	SET(optionalLibs ${optionalLibs} ${JPEG_LIBRARIES} )
	ADD_DEFINITIONS(-DENABLE_JPEG_SUPPORT)
ENDIF(JPEG_FOUND)

FIND_PACKAGE(PNG)
IF(PNG_FOUND)
	SET(optionalSources ${optionalSources} pngview.c)
	INCLUDE_DIRECTORIES( ${PNG_INCLUDE_DIR} )
	SET(optionalLibs ${optionalLibs} ${PNG_LIBRARIES} )
	ADD_DEFINITIONS(-DENABLE_PNG_SUPPORT)
ENDIF(PNG_FOUND)

ADD_EXECUTABLE(viewer ${mySources} ${optionalSources} )
TARGET_LINK_LIBRARIES(viewer ${optionalLibs})
