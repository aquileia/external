# externalVC

Dependency package for compiling Wesnoth on Visual C++

## Bundled archives

The version branches are referenced on the Wesnoth wiki  
http://wiki.wesnoth.org/CompilingWesnothOnWindows

Therefore we have to provide the following specific branch links:
- https://github.com/aquileia/external/archive/VC9.zip
- https://github.com/aquileia/external/archive/VC10.zip
- https://github.com/aquileia/external/archive/VC12.zip
- https://github.com/aquileia/external/archive/VC14.zip


## Updating Boost libraries

Download and unpack the source of the libraries zlib, libbzip2, boost (version 1.56 or 1.58+ preferred)
* http://www.bzip.org/downloads.html
* http://www.boost.org/users/download/
* http://www.zlib.net/

In the *Developer Command Prompt* that is installed with Visual Studio, go to the boost directory and type (with the correct paths of the other two libraries):
```
bootstrap
.\b2 -sZLIB_SOURCE=..\zlib-1.2.8 -sBZIP2_SOURCE=..\bzip2-1.0.6 -jN --with-date_time --with-filesystem --with-iostreams --with-locale --with-program_options --with-random --with-regex --with-system --with-thread
```
with **N** being the number of cores in your CPU (e.g. `-j4` for a quad core).
Depending on your boost version, you may need to replace `..\` with the absolute paths to zlib and bzip.
If you have multiple versions of Visual Studio installed, add `--toolset=msvc-X.0` with **X** being the target version number.

Separate the required subset of the Boost source:
```
.\b2 tools\bcp
dist\bin\bcp.exe algorithm asio assign bimap container date_time dynamic_bitset exception filesystem iostreams iterator locale math mpl multi_array multi_index program_options ptr_container random range regex serialization system test boost\nondet_random.hpp ..\..\_include
```

Replace the outdated files in 'external/lib' with those from 'boost_.../stage/lib' and those in 'external/include/boost' with  the ones in '_include/boost'.
