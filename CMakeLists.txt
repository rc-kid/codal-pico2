project(codal-pico2)

include("${CODAL_UTILS_LOCATION}")

# find sources and headers
RECURSIVE_FIND_DIR(TOP_LEVEL_INCLUDE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/inc" "*.h")
RECURSIVE_FIND_FILE(TOP_LEVEL_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/source" "*.c??")
RECURSIVE_FIND_FILE(TOP_LEVEL_C_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/source" "*.c")
RECURSIVE_FIND_DIR(MODEL_INCLUDE_DIRS "${CMAKE_CURRENT_SOURCE_DIR}/model" "*.h")
RECURSIVE_FIND_FILE(MODEL_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/model" "*.c??")

string(TOLOWER "${CODAL_TARGET_PROCESSOR}" TARGET_PROCESSOR)

# the cpu options (target.json cpu_opts) must also be used when linking so that the matching multilib is selected
set(CMAKE_LINKER_FLAGS "${CMAKE_LINKER_FLAGS} ${_CPU_COMPILATION_OPTIONS}" PARENT_SCOPE)
set(CMAKE_EXE_LINKER_FLAGS    "${CMAKE_EXE_LINKER_FLAGS} ${_CPU_COMPILATION_OPTIONS}" PARENT_SCOPE)
set(CMAKE_SYSTEM_PROCESSOR "cortex-m33" PARENT_SCOPE)

# add them
include_directories(${INCLUDE_DIRS} ${TOP_LEVEL_INCLUDE_DIRS} ${MODEL_INCLUDE_DIRS})

# create our target
add_library(codal-pico2 ${TOP_LEVEL_SOURCE_FILES} ${MODEL_SOURCE_FILES} ${TOP_LEVEL_C_SOURCE_FILES})

target_link_libraries(
    codal-pico2
    codal-rp2040
)

# expose it to parent cmake.
target_include_directories(codal-pico2 PUBLIC ${MODEL_INCLUDE_DIRS} ${TOP_LEVEL_INCLUDE_DIRS})
