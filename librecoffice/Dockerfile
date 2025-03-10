# syntax = docker/dockerfile:1
FROM debian:stable-slim AS builder

ENV DEBIAN_FRONTEND=noninteractive

# 使用国内源，加快下载速度
RUN echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian stable main contrib non-free" > /etc/apt/sources.list && \
    echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian-security stable-security main contrib non-free" >> /etc/apt/sources.list

# 更新并安装 LibreOffice 和所需语言包
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        curl \
        libreoffice \
        tzdata \
        python3-pip && \
    ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

## 安装语言包
#RUN for LOCALE in $(curl -sL https://raw.githubusercontent.com/thelamer/lang-stash/master/langs); do \
#      apt-get install -y --no-install-recommends libreoffice-lang-$(echo ${LOCALE}| tr '[:upper:]' '[:lower:]') || apt-get install -y --no-install-recommends libreoffice-lang-$(echo ${LOCALE}| head -c2); \
#    done && \
#    apt-get clean && \
#    rm -rf /var/lib/apt/lists/*

# 安装unoconvert.go
# https://github.com/unoconv/unoserver#installation
#RUN curl -k -L -o find_uno.py https://gist.githubusercontent.com/regebro/036da022dc7d5241a0ee97efdf1458eb/raw/find_uno.py && \
#   python3 find_uno.py
#RUN curl -k -L https://bootstrap.pypa.io/get-pip.py && \
#    python3 get-pip.py && \
#    python3 -m pip install unoserver
RUN pip3 install --no-cache unoserver==3.0.1 --break-system-packages

# 验证 LibreOffice 和 unoconvert 版本
RUN libreoffice --headless --version
RUN unoserver -v
