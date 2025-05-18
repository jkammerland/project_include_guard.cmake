# project_include_guard

A CMake module providing a robust include guard mechanism with version checking.

## Overview

`project_include_guard` prevents multiple inclusions of the same CMake module while performing version compatibility checks. This helps detect potential issues when mixing different versions of the same module in complex CMake projects.

## Features

- Prevents multiple inclusions of the same module
- Checks version compatibility between included modules
- Issues warnings for potential version compatibility issues
- Fails with a clear error on major version mismatches

## Requirements

- CMake 3.20 or higher
- `PROJECT_NAME`, `PROJECT_VERSION` must be defined

## Using fetchcontent

```cmake
# Get the project_include_guard package
include(FetchContent)
FetchContent_Declare(
    project_include_guard
    GIT_REPOSITORY https://github.com/jkammerland/project_include_guard.cmake.git
    GIT_TAG v1.1.0 # or branch/commit
)
FetchContent_MakeAvailable(project_include_guard)

# Now you can use project_include_guard()
```

## Using CPM

```cmake
cpmaddpackage("gh:jkammerland/project_include_guard.cmake@1.1.0")
```

## Manual Installation

Alternatively, you can include the module directly:

1. Download file/repo
2. Include the `project_include_guard.cmake` file in your project

## Usage

```cmake
# In your CMake module
project(my_module VERSION 1.2.3)

# e.g
include(${CMAKE_CURRENT_SOURCE_DIR}/cmake/project_include_guard.cmake)
project_include_guard()

# Rest of your module code...
```

## Behavior

- **Fatal Error**: Major version mismatch detected
- **Warning**: Including a newer version than previously used. Forward compatibility issues may exist.
- **Verbose Log**: Including an older version or first-time inclusion. Always guarantee backwards compatibility within the same major version.
