
# Build the query module
INCLUDE_DIRECTORIES(
	${PYTHON_INCLUDE_PATH}
)

ADD_LIBRARY(query SHARED
	DefaultPatternMatchCB.cc
	PatternMatch.cc
	PatternMatchEngine.cc
	QueryModule.cc
)

ADD_DEPENDENCIES(query
	opencog_atom_types
)

IF (HAVE_GUILE)
	# TARGET_LINK_LIBRARIES(query smob)
ENDIF (HAVE_GUILE)

IF (HAVE_CYTHON)
	TARGET_LINK_LIBRARIES(query ${PYTHON_LIBRARY})
ENDIF (HAVE_CYTHON)

IF (WIN32)
   INSTALL (TARGETS query DESTINATION "lib${LIB_DIR_SUFFIX}/opencog")
ELSEIF (CYGWIN)
   INSTALL (TARGETS query DESTINATION "lib${LIB_DIR_SUFFIX}/opencog")
ENDIF (WIN32)

INSTALL (FILES
	CrispLogicPMCB.h
	DefaultPatternMatchCB.h
	OutgoingTree.h
	PatternMatch.h
	PatternMatchCallback.h
	PatternMatchEngine.h
	QueryModule.h
	DESTINATION "include/${PROJECT_NAME}/query"
)
