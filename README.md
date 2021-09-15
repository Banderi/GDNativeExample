## GDNativeExample
This is the official [GDNative C example project](https://docs.godotengine.org/en/3.3/tutorials/plugins/gdnative/gdnative-c-example.html) (headers for Godot v3.3.stable), made to work as a CLion-compatible (CMakeLists.txt) project. It compiles and runs successfully under Windows.

***This does NOT work with the [C++ version of GDNative](https://docs.godotengine.org/en/3.3/tutorials/plugins/gdnative/gdnative-cpp-example.html), which requires SCons to generate the CPP bindings.***

The IDE can also be made to run the game directly on debug by setting the following:
- Executable to run: `[path to Godot executable]`
- Working directory: `<.../GDNativeExample/project/>`

E.g. here's on my CLion settings:
![image](https://user-images.githubusercontent.com/16541079/133392093-11092cb8-a6c3-4123-8d32-818b8cfc5be1.png)
