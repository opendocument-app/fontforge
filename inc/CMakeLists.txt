# Distributed under the original FontForge BSD 3-clause license

add_library(fontforge_common_headers INTERFACE)

include(FontForgeConfigure)
fontforge_generate_config(fontforge-config.h.in fontforge-config.h)
fontforge_generate_version_extras(fontforge-version-extras.h.in fontforge-version-extras.h)

target_include_directories(fontforge_common_headers
  INTERFACE
    "${CMAKE_CURRENT_SOURCE_DIR}"
    "${CMAKE_CURRENT_BINARY_DIR}"
)

target_link_libraries(fontforge_common_headers
  INTERFACE
    glib::glib
)

if(ENABLE_CODE_COVERAGE_RESULT)
target_link_libraries(fontforge_common_headers
  INTERFACE
    Gcov::Gcov
)
endif()

set(FONTFORGE_COMMON_INST_HEADERS
  "${CMAKE_CURRENT_BINARY_DIR}/fontforge-config.h"
  "${CMAKE_CURRENT_BINARY_DIR}/fontforge-version-extras.h"
  basics.h
  carbon.h
  dlist.h
  ffgdk.h
  ffglib.h
  gdraw.h
  gfile.h
  ggadget.h
  gicons.h
  gimage.h
  gkeysym.h
  gprogress.h
  gresedit.h
  gresource.h
  gutils.h
  gwidget.h
  gwwiconv.h
  hotkeys.h
  intl.h
  prefs.h
  ustring.h
  utype.h
)
set_target_properties(fontforge_common_headers PROPERTIES PUBLIC_HEADER "${FONTFORGE_COMMON_INST_HEADERS}")

install(TARGETS fontforge_common_headers
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
)
