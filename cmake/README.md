Main directory of `cmake` modules.

### Manual add
Modules can be included manually:
```cmake
set(SUGAR_ROOT "/path/to/sugar/root/directory")
list(APPEND CMAKE_MODULE_PATH "${SUGAR_ROOT}/cmake/core")

include(sugar_foo) # sugar_foo.cmake searched in core directory
```

### Master file 
Modules can be included automatically by master file [Sugar](https://github.com/ruslo/sugar/blob/master/cmake/Sugar):
```cmake
# assuming that GITENV_ROOT environment variable is set
include($ENV{GITENV_ROOT}/sugar/cmake/Sugar)

include(sugar_foo) # sugar_foo.cmake searched in all directories: core, print, utility, ...
```
in this case
* all directories (core, utility, print, ...) will be added to [CMAKE_MODULE_PATH](http://www.cmake.org/cmake/help/v2.8.11/cmake.html#variable:CMAKE_MODULE_PATH)
* `SUGAR_ROOT` *cmake* variable will be setted
* `SUGAR_ROOT` variable will be printed using `message` command:
<pre>
-- The C compiler identification is Clang 5.0.0
-- The CXX compiler identification is Clang 5.0.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
SUGAR_ROOT: /.../gitenv/sugar
-- Configuring done
-- Generating done
-- Build files have been written to: /.../gitenv/sugar/examples/00-detect/_builds/make-default
</pre>