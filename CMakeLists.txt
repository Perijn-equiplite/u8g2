#
#  U8g2 component for ESP-IDF + Arduino-as-component
#

# 1) Collect every source file the library has
file(GLOB_RECURSE U8G2_C_SRC   "csrc/*.c")
file(GLOB_RECURSE U8G2_CPP_SRC "cppsrc/*.cpp")

# 2) Register the component
idf_component_register(
    SRCS          ${U8G2_C_SRC} ${U8G2_CPP_SRC}
    INCLUDE_DIRS  csrc cppsrc
    REQUIRES      arduino-esp32        # pulls in Arduino headers & core
)

# 3) The C helpers are compiled only if ARDUINO is defined
target_compile_definitions(${COMPONENT_LIB} PRIVATE ARDUINO=10805)

# 4) (Optional) silence a few benign warnings that turn into errors at –Werror
target_compile_options(${COMPONENT_LIB} PRIVATE
    -Wno-sign-compare -Wno-unused-parameter -Wno-missing-field-initializers
)
