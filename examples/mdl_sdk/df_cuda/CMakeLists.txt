# name of the target and the resulting example
set(PROJECT_NAME mdl_sdk_example-df_cuda)

# -------------------------------------------------------------------------------------------------
# Main Target 
# -------------------------------------------------------------------------------------------------

# collect sources
set(PROJECT_SOURCES
    "example_df_cuda.cpp"
    "example_df_cuda.h"
    )

# create target from template
create_from_base_preset(
    TARGET ${PROJECT_NAME}
    TYPE EXECUTABLE
    NAMESPACE mdl_sdk_examples
    SOURCES ${PROJECT_SOURCES}
)

# add dependencies
target_add_dependencies(TARGET ${PROJECT_NAME}
    DEPENDS
        mdl::mdl_sdk
        mdl_sdk_examples::mdl_sdk_shared
        opengl
        imgui
        cuda
    )

# creates a user settings file to setup the debugger (visual studio only, otherwise this is a no-op)
target_create_vs_user_settings(TARGET ${PROJECT_NAME})

# -------------------------------------------------------------------------------------------------
# PTX Target 
# -------------------------------------------------------------------------------------------------
target_add_cuda_ptx_rule(TARGET ${PROJECT_NAME} 
    DEPENDS 
        mdl::mdl_sdk
        mdl_sdk_examples::mdl_sdk_shared
    CUDA_SOURCES
        "example_df_cuda.cu"
    )
