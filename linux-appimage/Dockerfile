FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

# Create a user account citra (UID 1027) that the container will run as
RUN useradd -m -u 1027 -s /bin/bash citra

# Update system, install PPAs and install packages for building Citra.
RUN apt-get update && apt-get full-upgrade -y
RUN apt-get install -y software-properties-common lsb-release
RUN add-apt-repository -y ppa:savoury1/build-tools && \
    add-apt-repository -y ppa:savoury1/display && \
    add-apt-repository -y ppa:savoury1/ffmpeg4 && \
    add-apt-repository -y ppa:savoury1/gcc-defaults-11 && \
    add-apt-repository -y ppa:savoury1/llvm-defaults-13 && \
    add-apt-repository -y ppa:savoury1/qt-6-2 && \
    add-apt-repository -y ppa:theofficialgman/gpu-tools
RUN apt-get update && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt-get install -y \
    build-essential \
    libsdl2-dev \
    libssl-dev \
    clang \
    lld \
# Qt 5
    qtbase5-dev \
    qtbase5-private-dev \
    libqt5opengl5-dev \
    qtmultimedia5-dev \
    qttools5-dev \
    qttools5-dev-tools \
    qt5-gtk-platformtheme \
    qt5ct \
    qt5-style-plugins \
    libqt5opengl5-dev \
    libqt5multimedia5-plugins \
# Qt 6
    qt6-base-dev \
    qt6-base-private-dev \
    qt6-multimedia-dev \
    qt6-l10n-tools \
    qt6-tools-dev \
    qt6-tools-dev-tools \
    qt6-gtk-platformtheme \
    qt6-documentation-tools \
    qt6-wayland \
# FFmpeg
    ffmpeg \
    libavcodec-dev \
    libavdevice-dev \
    libavfilter-dev \
    libavformat-dev \
    libswresample-dev \
    libswscale-dev \
# Tools
    cmake \
    p7zip-full \
    wget \
    unzip \
    git \
    ccache \
    ninja-build \
    glslang-dev \
    glslang-tools \
    file

# Install glslang
RUN cd /tmp && \
    wget https://github.com/KhronosGroup/glslang/releases/download/main-tot/glslang-main-linux-Release.zip && \
    unzip glslang-main-linux-Release.zip -d glslang && \
    cp -rv glslang/* /usr && \
    rm -rf glslang-*

# Download tools for building AppImages
RUN wget https://github.com/linuxdeploy/linuxdeploy/releases/download/continuous/linuxdeploy-x86_64.AppImage && \
    wget https://github.com/linuxdeploy/linuxdeploy-plugin-qt/releases/download/continuous/linuxdeploy-plugin-qt-x86_64.AppImage && \
    wget https://github.com/linuxdeploy/linuxdeploy-plugin-checkrt/releases/download/continuous/linuxdeploy-plugin-checkrt-x86_64.sh && \
    chmod a+x linuxdeploy-x86_64.AppImage && \
    chmod a+x linuxdeploy-plugin-qt-x86_64.AppImage && \
    chmod a+x linuxdeploy-plugin-checkrt-x86_64.sh
