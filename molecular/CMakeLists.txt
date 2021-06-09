
add_library( MolecularEngine OBJECT MolecularWorld.cpp MoleculeType.cpp AtomTypes.cpp  )

file(GLOB molecular_HEADERS_ *.h )
add_custom_target(molecular_headers SOURCES ${molecular_HEADERS_} )
