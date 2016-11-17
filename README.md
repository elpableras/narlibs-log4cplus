# narlibs-log4cplus
Building LOG4CPLUS from source via CMake and packaging as NAR for reuse.

Using the Maven NAR plugin, you can then simply add NAR dependencies to your build - Log4cplus headers and binaries 
will automatically be integrated in your build.

# Release Notes

## Version 1.2.0.1

Upstream log4cplus version 1.2.0.1

Note that v 1.2.0 had issues running on W7 SP1, v 1.2.0.1 was recompiled with MSVC 12 and seems to work as expected.

Built on :
* CERN CentOS 7 - gcc 4.8.5, libstdc++ 6, pthread
* Windows 7 64 bits - MSVC 12 (MS Visual Studio 13)
