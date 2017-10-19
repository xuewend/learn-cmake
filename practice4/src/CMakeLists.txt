ADD_EXECUTABLE(main main.c)
INCLUDE_DIRECTORIES(/usr/include/hello)
TARGET_LINK_LIBRARIES(main libhello.a)
