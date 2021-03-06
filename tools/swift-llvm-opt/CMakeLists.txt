add_swift_host_tool(swift-llvm-opt
  LLVMOpt.cpp
  SWIFT_COMPONENT tools
)
target_link_libraries(swift-llvm-opt
                      PRIVATE
                        swiftIRGen
                        # Swift libraries included to appease the linker on linux.
                        swiftSema
                        swiftAST
                      )
if(SWIFT_LINK_SHARED_CLANG)
  target_link_libraries(swift-llvm-opt PRIVATE
                        clang-cpp
                        LLVM
                        )
else()
  target_link_libraries(swift-llvm-opt PRIVATE
                        # Clang libraries included to appease the linker on linux.
                        clangBasic
                        clangCodeGen
                        # LLVM libraries included to appease the linker on linux.
                        LLVMAggressiveInstCombine
                        LLVMCodeGen
                        LLVMInstCombine
                        LLVMScalarOpts
                        LLVMVectorize
                        )
endif()
