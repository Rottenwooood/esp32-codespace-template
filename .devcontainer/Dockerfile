FROM ubuntu:20.04

# 设置非交互模式
ENV DEBIAN_FRONTEND=noninteractive

# 安装基础依赖
RUN apt-get update && apt-get install -y \
    git wget flex bison gperf python3 python3-pip python3-setuptools \
    cmake ninja-build ccache libffi-dev libssl-dev dfu-util libusb-1.0-0 \
    tzdata

# 设置默认时区
RUN ln -fs /usr/share/zoneinfo/Etc/UTC /etc/localtime && \
    dpkg-reconfigure -f noninteractive tzdata

# 安装 ESP-IDF
ENV IDF_PATH=/esp-idf
RUN git clone --recursive https://github.com/espressif/esp-idf.git $IDF_PATH && \
    test -f $IDF_PATH/requirements.txt || (echo "requirements.txt not found!" && exit 1)

# 安装 Python 依赖
RUN python3 -m pip install --upgrade pip && \
    python3 -m pip install --user -r $IDF_PATH/requirements.txt

# 设置环境变量
ENV PATH="$IDF_PATH/tools:$PATH"

# 设置工作目录
WORKDIR /workspace