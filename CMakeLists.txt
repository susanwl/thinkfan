project(thinkfan)

option(USE_ATASMART "Enable reading temperatures from HDDs via S.M.A.R.T")
set(MAXERR 2 CACHE STRING "Fail after this many consecutive errors when in DANGEROUS
mode")

add_executable(thinkfan thinkfan.c config.c message.c parser.c system.c)

set(CMAKE_C_FLAGS_DEBUG "-O0 -g3 -Wall -DDEBUG")
set(CMAKE_C_FLAGS "-O3 -Wall")

if(MAXERR)
	set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -DMAXERR=${MAXERR}")
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DMAXERR=${MAXERR}")
endif(MAXERR)

if(USE_ATASMART)
	set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -DUSE_ATASMART")
	set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -DUSE_ATASMART")
	target_link_libraries(thinkfan atasmart)
endif(USE_ATASMART)