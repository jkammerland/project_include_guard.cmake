# project_include_guard

A CMake module providing a robust include guard mechanism with version checking, both at the **project** and **file** level. The problem with the standard `include_guard(GLOBAL/DIRECTORY)` is that it cannot track versions, or specific file ids, and can therefore create extremely hard to debug problems with no feedback whatsoever from cmake.

## Usage

### File-level Include Guard

```cmake
# In your individual CMake file
list_file_include_guard(VERSION 1.2.4)
```

### Project-level Include Guard

```cmake
# In your CMake module
project(my_module VERSION 1.2.4)

# protect the project against being added again
# (e.g add_subdirectory / submodules / inlined deps)
project_include_guard()
```

> [!IMPORTANT]
> This will prevent the `filename/ID` from being included multiple times, even if it's in different directories. This assumes that the "same file" has not been renamed!

>[!NOTE]
> The default behavior of a redefinition function is to overwrite the previous definition (e.g from multiple includes). This can happen if you use fetchcontent alot from selfcontained projects that has similar includes. This will can cause lower projects to overwrite functions GLOBALLY because a functions/macros always have a global scope. The solution to this is some form of include guard when defining functions/macros.

>[!IMPORTANT]
> the standard include_guard(GLOBAL/DIRECTORY) works on a per-file basis, not per filename/ID. This means it does not protect you from another project including their own version of a function/macros which has already been defined by another project. Thus overwritting them globally. This behavior is can be replicated by this function like this: 

```cmake
# Now it works the same as include_guard(), 
# and the version is redundant because the guard only works with the SAME FILE anyway.
list_file_include_guard(VERSION 1.4.0 ID ${CMAKE_CURRENT_LIST_FILE})
```

---

## Overview

`list_file_include_guard` works on individual cmake files, while also tracking it's version. Note that the scope is ALWAYS GLOBAL, unlike the standard `include_guard` which can be set to DIRECTORY for example. This could be a future improvement.

`project_include_guard` prevents multiple inclusions of the same CMake module while performing version compatibility checks. This helps detect potential issues when mixing different versions of the same module in complex CMake projects. This is useful for preventing multiple inclusions from add_subdirectory (which IMO should never happen anyway, unless you are using git submodules or manual methods). It uses `list_file_include_guard` internally.

---

## Features

- **Project-level include guard**: Prevents multiple inclusions of the same module.
- **File-level include guard**: Prevents multiple inclusions of the same file with version checking.
- **Version compatibility checks**:
  - Fails with a clear error on **major version mismatch**.
  - Issues a **warning** if a **newer minor version** is included, i.e the "y" in x.y.z.
  - Logs **verbosely** if an **older version** is included.

---

## Requirements

- **CMake 3.20 or higher**

---

## Installation

### Using fetchcontent

```cmake
# Get the project_include_guard package
include(FetchContent)
FetchContent_Declare(
    project_include_guard
    GIT_REPOSITORY https://github.com/jkammerland/project_include_guard.cmake.git
    GIT_TAG v1.2.4 # or branch/commit
)
FetchContent_MakeAvailable(project_include_guard)

# Now you can use project_include_guard() and list_file_include_guard(VERSION x.y.z)
```

### Using CPM

```cmake
cpmaddpackage("gh:jkammerland/project_include_guard.cmake@1.2.4")
```

### Manual Installation

Alternatively, you can include the module directly:

1. Download the repository or individual files
2. Include the `project_include_guard.cmake` and `list_file_include_guard.cmake` files in your project

---

## Behavior

- **Fatal Error**: Major version mismatch detected
- **Warning**: Including a newer version than previously used. Forward compatibility issues may exist.
- **Verbose Log**: Including an older version or first-time inclusion. Always guarantee backwards compatibility within the same major version.