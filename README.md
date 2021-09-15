## GDNativeExample
This is the official [GDNative C example project](https://docs.godotengine.org/en/3.3/tutorials/plugins/gdnative/gdnative-c-example.html) from [here](https://github.com/godotengine/gdnative-demos/tree/master/c/simple) (headers for Godot v3.3.stable from [here](https://github.com/godotengine/godot-headers/tree/3.3)), made to work as a CLion-compatible (CMakeLists.txt) project. It compiles and runs successfully under Windows.

CMakeLists.txt script:
```CMake
cmake_minimum_required(VERSION 3.17)
project(GodotNeuralNetworkTests2)

set(CMAKE_CXX_STANDARD 14)
include_directories(${PROJECT_SOURCE_DIR}/godot-headers)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ../project/gdnative/windows)

add_library(simple SHARED src/simple.c)
```

***This does NOT work with the [C++ version of GDNative](https://docs.godotengine.org/en/3.3/tutorials/plugins/gdnative/gdnative-cpp-example.html), which requires SCons to generate the CPP bindings.***

---

### Library debugging from IDE
The IDE can also be made to run the game directly on debug by setting the following:
- Executable to run: `[path to Godot executable]`
- Working directory: `<.../GDNativeExample/project/>`

E.g. here's on my CLion settings:
![image](https://user-images.githubusercontent.com/16541079/133392093-11092cb8-a6c3-4123-8d32-818b8cfc5be1.png)

---

### Library load/execution failure in Godot
For GDNative coding in general - there may be cases of the code perfectly compiling, but the library fails to load in the Godot project. This results in the infamous ***Error 126** ("The specified module could not be found")* which gives back little to no information over the cause of the issue.

In the engine, it usually looks like failure on the `load("res://<library_res_file_path>.gdns").new()` line which throws the `Attempt to call function 'new' in base 'NativeScript' on a null instance.` error.

This error can be very annoying since it's very opaque and requires lots of trial and error to narrow down the culprit. From my experiments, I've found a couple of possible causes:
- Failure to run `godot_gdnative_init` and/or registration of the library's class structure
- Compiling the library init code as C++ instead of C (e.g. renaming "simple.c" to "simple.cpp")
- Inclusion and usage of incompatible C++ mechanisms, like `std::vector`
- Invalid `extern`s which can be solved by using instead the following syntax:
    ```c++
    #ifdef __cplusplus
    #define CEXTERN extern "C"
    #else
    #define CEXTERN
    #endif
    ```
