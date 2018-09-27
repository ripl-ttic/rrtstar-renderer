find_package(PkgConfig REQUIRED)
pkg_check_modules(BOT2_VIS bot2-vis)

add_definitions(-std=gnu99)

add_library(rrtstar-renderer SHARED
            renderer_rrtstar.c)

target_link_libraries(rrtstar-renderer ${OPENGL_LIBRARIES})

set(REQUIRED_LIBS bot2-vis lcmtypes_rrtstar)

pods_use_pkg_config_packages(rrtstar-renderer ${REQUIRED_LIBS})

pods_install_headers(renderer_rrtstar.h DESTINATION rrtstar_renderer)
pods_install_libraries(rrtstar-renderer)
pods_install_pkg_config_file(rrtstar-renderer
    CFLAGS
    LIBS -lrrtstar-renderer
    REQUIRES ${REQUIRED_LIBS}
    VERSION 0.0.1)
