message("Configuring libCGAL_Core")

use_essential_libs()

include_directories (SYSTEM ${CGAL_3RD_PARTY_INCLUDE_DIRS})

add_definitions(${CGAL_3RD_PARTY_DEFINITIONS})

link_directories    ( ${CGAL_LIBRARIES_DIR} ${CGAL_3RD_PARTY_LIBRARIES_DIRS} )

collect_cgal_library(CGAL_Core "")

if(NOT CGAL_HEADER_ONLY)
   # CGAL_Core does not depend on CGAL in either DEBUG or RELEASE, but we
   # still link it.
   target_link_libraries( CGAL_Core CGAL ${CGAL_3RD_PARTY_LIBRARIES} )

   add_dependencies( CGAL_Core CGAL )
else()
  target_link_libraries( CGAL_Core INTERFACE ${CGAL_3RD_PARTY_LIBRARIES} )
endif()

set(EXPORT_TARGETS ${EXPORT_TARGETS} PARENT_SCOPE)

message("libCGAL_Core is configured")

