<!--
Title: CMake - Add library to browse
Author: Jacob Moen
Date: 2017/05/25 11:53
Datetime: 2017-05-24
Description: Sometimes you want to be able to browse the source code of a library without adding it to your CMake project
View: post
ogimage: cmake-browse/cmakebrowse.jpeg
thumb: cmake-browse/cmakebrowse_custom.jpeg
Keywords: cmake, trick, project, library, programming, c
Tags: cmake, programming, c
blogpost: true
published: false
-->
(inimage:CMake Trick source:cmake-browse/cmakebrowse.jpeg)

It happens often: I want to be able to browse not only the interface, but also the actual source code, for a library that I use in a project.

There are not a lot of options here. Either you add it to your project physically, by moving the files into your source tree, or you configure your IDE/editor to include source code when browsing external libraries.

The second option will cause your editor to indiscriminately go and index the source code for each and every library that your project uses.

(clearfix:)

I wished there was a third option, and there is!

And it only takes a small, non-intrusive CMake hack.

## Add library hack

If you read the CMake documentation for [add_library](https://cmake.org/cmake/help/v3.0/command/add_library.html), you will learn that you can add a library to your project, with headers and sources, and a StackOverflow [answer](https://stackoverflow.com/questions/34453476/clion-add-dependency-headers-and-sources) suggested that it can be used/abused to allow your IDE to browse the source code for it.

And I just had to try it!

### Code example

I am working on a project that uses a library that I am developing.

Therefore I want to not only be able to browse the interface, but also the implementation.

And I don't want to copy the library into my source tree.

So, I added  the following lines of code to my CMake script:

```cmake
set(NASL_SOURCECODE /home/jacmoe/.conan/data/nasl/0.4/jacmoe/testing/source/nasl/)

set(NASL_HEADERS
${NASL_SOURCECODE}/include/nasl_defs.h
${NASL_SOURCECODE}/include/nasl_dbg.h
[...]
)

set(NASL_SOURCES
${NASL_SOURCECODE}/src/nasl_script.c
${NASL_SOURCECODE}/src/nasl_graphics.c
[...]
)

add_library(nasl ${NASL_HEADERS} ${NASL_SOURCES})
```

## It works ?

Yes! it actually works.

CLion warns me that I have source code outside of the CMake root, but it works: I am able to browse my external library properly.

I haven't tried it on a 'dirty' library, though, as that might trigger a rebuild of it, and that would probably fail.