

## What Does `Cmake ..` do?



cmake is a Makefile generator.

When you call `cmake [path]`, you ask it to generate a Makefile in the current directory following instructions given in `[path]/CMakeLists.txt`

Usually `cmake` output some messages while it is working, and after it is done without errors, you can type "make" to execute your newly created Makefile.

`CMakeLists.txt` files can reference other `CMakeLists.txt` file in sub-directories, so you are usually only interested by the `CMakeLists.txt` of the top directory, not the other ones.

Using an empty `build` directory is a technique called `out-of-source build`, in which all your generated files `(.o, executable, Makefile, .anything)` are generated in the separate `build` directory and not mixed with source files. If you want to clean all, you can delete all the content of the build directory.
`
In fact, you can put your `build` directory in any place, as long as you give cmake the correct path of the top `CMakeLists.txt`. You can even have several build directories. It is very useful if you need several different builds at the same time (with different options, different versions of gcc, etc.)

In old programs, you generate the Makefile too, but using `./configure `(this is called auto-tools. You may have encountered that already). `cmake` is considered a successor of the auto-tools.
