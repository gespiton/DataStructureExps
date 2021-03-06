cmake_minimum_required(VERSION 3.5)
add_library(DsExpLib 
StrException.h StrException.cpp
SparseMatrix.hpp
BFS.h BFS.cpp
ExpressionTree.h ExpressionTree.cpp
ExpressionStack.h ExpressionStack.cpp
BinaryTree.hpp
Dijkstra.h Dijkstra.cpp
Kruskal.h Kruskal.cpp
AVL.hpp
)

if (COVERALLS)
    set(COVERAGE_SRCS
		src/StrException.cpp
		src/SparseMatrix.hpp
		src/BFS.cpp
		src/ExpressionTree.cpp
		src/ExpressionStack.cpp
		src/BinaryTree.hpp
		src/Dijkstra.h src/Dijkstra.cpp
		src/Kruskal.h src/Kruskal.cpp
		src/AVL.hpp
	)

    # Create the coveralls target.
    coveralls_setup(
        "${COVERAGE_SRCS}" # The source files.
        ${COVERALLS_UP}     ) # If we should upload.
endif()

if(USE_FOLDEXP)
  target_compile_definitions(DsExpLib PRIVATE Use_FoldExp)
endif()

if(USE_WCOUT)
  target_compile_definitions(DsExpLib PRIVATE Use_Wcout)
endif()

if(NOT ENABLE_SparseMatrix)
  target_compile_definitions(DsExpLib PRIVATE SparseMatrix_disabled)
  set(ENABLE_Dijkstra false CACHE BOOL "If Dijkstra  enabled. " FORCE)
  set(ENABLE_Kruskal false CACHE BOOL "If Kruskal enabled. " FORCE)
endif()

if(NOT ENABLE_BFS)
  target_compile_definitions(DsExpLib PRIVATE BFS_disabled)
endif()

if(NOT ENABLE_ExpressionTree)
  target_compile_definitions(DsExpLib PRIVATE ExpressionTree_disabled)
endif()

if(NOT ENABLE_ExpressionStack)
  target_compile_definitions(DsExpLib PRIVATE ExpressionStack_disabled)
endif()

if(NOT ENABLE_Dijkstra)
  target_compile_definitions(DsExpLib PRIVATE Dijkstra_disabled)
endif()

if(NOT ENABLE_BinaryTree)
  target_compile_definitions(DsExpLib PRIVATE BinaryTree_disabled)
  set(ENABLE_AVL false CACHE BOOL "If AVL enabled." FORCE)
endif()

if(NOT ENABLE_Kruskal)
  target_compile_definitions(DsExpLib PRIVATE Kruskal_disabled)
endif()

if(NOT ENABLE_AVL)
  target_compile_definitions(DsExpLib PRIVATE AVL_disabled)
endif()
