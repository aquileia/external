# externalVC

Dependency package for compiling Wesnoth on Visual C++

## Bundled archives

The version branches are referenced on the Wesnoth wiki  
http://wiki.wesnoth.org/CompilingWesnothOnWindows

Therefore we have to provide the following specific branch links:
- https://github.com/aquileia/external/archive/VC10.zip
- https://github.com/aquileia/external/archive/VC12.zip


## Updating Boost libraries

Download and unpack the source of the libraries zlib, libbzip2, boost (version 1.56 or 1.58+ preferred)
* http://www.bzip.org/downloads.html
* http://www.boost.org/users/download/
* http://www.zlib.net/

In the *Developer Command Prompt* that is installed with Visual Studio, go to the boost directory and type (with the correct paths of the other two libraries):
```
bootstrap
.\b2 -sZLIB_SOURCE=..\zlib-1.2.8 -sBZIP2_SOURCE=..\bzip2-1.0.6 -jN --with-locale --with-regex --with-filesystem --with-system --with-program_options --with-random --with-thread
```
with **N** being the number of cores in your CPU (e.g. `-j4` for a quad core).

Separate the required subset of the Boost source:
```
.\b2 tools\bcp
dist\bin\bcp.exe filesystem locale iostreams multi_index random regex serialization asio program_options system date_time ptr_container ..\..\_include
```

Replace the outdated files in 'external/lib' with those from 'boost_.../stage/lib' and those in 'external/include/boost' with  the ones in '_include/boost'.
