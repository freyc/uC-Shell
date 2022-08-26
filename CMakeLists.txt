
add_library(uC-Shell STATIC
    Source/shell.c
    Source/shell.h
    Cmd/General/sh_shell.c
    Cmd/General/sh_shell.h)

if(UCSHELL_TERMINAL_SUPPORT)
    target_sources(uC-Shell PRIVATE 
        Terminal/Source/terminal.c
        Terminal/Source/terminal.h
        Terminal/Mode/VT100/terminal_mode.c)
    target_include_directories(uC-Shell PUBLIC Terminal/Source)
    target_compile_definitions(uC-Shell PUBLIC -DUCSHELL_HAVE_TERMINAL=1)
endif()

target_include_directories(uC-Shell PUBLIC 
    Source
    Cmd/General
    ${UCSHELL_CFG_DIR})

target_link_libraries(uC-Shell PUBLIC uC-CPU uC-LIB)