# 在项目中使用 FFmpeg 库

### 一、引言

首先需要把 `FFmpeg` 安装到指定路径，安装过程。安装可参考官方指南：[https://trac.ffmpeg.org/wiki/CompilationGuide](https://trac.ffmpeg.org/wiki/CompilationGuide)。

要使用 `FFmpeg` 就必须引用它的头文件，以及在链接中使用它的静态或动态库文件。

本文即是讲述关于如何引用该库的头文件以及使用 `CMake` 来链接库文件构建项目。

### 二、在项目文件中引用头文件

面向对象的 `C++` 本身是支持函数重载的，而面向过程的 `C` 语言不支持重载。

不同的设计理念使得同一个函数在两种语言编译后的符号表中的签名是不同的，进而在链接过程中如果不加 `extern "C"` 关键字将会链接到 `C++` 格式的方法签名，而加了 `extern "C"` 关键字会寻找 `C` 格式的方法签名。

`FFmpeg` 是 `C` 语言书写的，所以我们在 `C++` 项目中引用 `FFmpeg` 时必须加上 `extern "C"` 关键字。

```c++
/**
 * Main file: main.cc
 *
 * Description:
 *	Try to do some avcodec operations by invoking functions defined in ffmpeg.
 */

#include <cstdio>

#ifdef __APPLE__
extern "C" {
#include "libavcodec/avcodec.h"
#include "libavformat/avformat.h"
#include "libswscale/swscale.h"
#include "libswresample/swresample.h"
#include "libavutil/pixdesc.h"
}
#endif

int main(const int argc, char* argv[])
{
    avformat_network_init();

    if (argc < 2) {
        printf("Please set the file path to open...\n");
        exit(0);
    }
    printf("open accompany file %s ...\n", argv[1]);

    AVFormatContext *formatCtx = avformat_alloc_context();

    // Do something

    return 0;
}
```

### 三、设置并链接相应的库

在 `CMakeLists.txt` 中使用 `INCLUDE_DIRECTORIES` 设置 `FFmpeg` 头文件所在路径。

使用 `LINK_DIRECTORIES` 设置库文件所在路径，并在 `TARGET_LINK_LIBRARIES` 中链接所需要的库文件。

```python
# CMakeLists.txt
CMAKE_MINIMUM_REQUIRED(VERSION 3.0)

PROJECT(FFMPEG_TEST)

SET(CMAKE_BUILD_TYPE RELEASE)
SET(CMAKE_CXX_STANDARD 11)
SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11 -Wall")
SET(FFmpeg_DIR /Users/phillee/ffmpeg)

INCLUDE_DIRECTORIES(${FFmpeg_DIR}/ffmpeg-bin/include)
LINK_DIRECTORIES(${FFmpeg_DIR}/ffmpeg-bin/lib)

# Messages to show
MESSAGE(STATUS "** Customized settings are shown as below **")
MESSAGE(STATUS "\tCMAKE BUILD TYPE: ${CMAKE_BUILD_TYPE}")
MESSAGE(STATUS "\tFFmpeg include directory: ${FFmpeg_DIR}/ffmpeg-bin/include")
MESSAGE(STATUS "\tFFmpeg library directory: ${FFmpeg_DIR}/ffmpeg-bin/lib")

ADD_EXECUTABLE(ffmpeg_test main.cc)

TARGET_LINK_LIBRARIES(ffmpeg_test
    avcodec
    avformat
    avutil
    postproc
    swresample
    swscale
    )
```

设置完成后 `cmake` 和 `make` 编译即可成功生成可执行文件。

```bash
$ mkdir build && cd build

$ cmake .. && make
```
