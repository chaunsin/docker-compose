# syntax = docker/dockerfile:1
FROM alpine:3.21 AS builder

#ENV DEBIAN_FRONTEND=noninteractive

# 使用国内源，加快下载速度
# RUN echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian stable main contrib non-free" > /etc/apt/sources.list && \
#    echo "deb http://mirrors.tuna.tsinghua.edu.cn/debian-security stable-security main contrib non-free" >> /etc/apt/sources.list
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.ustc.edu.cn/g' /etc/apk/repositories

# 更新并安装 LibreOffice 和所需语言包
#RUN apt-get update && \
#    apt-get install -y --no-install-recommends \
#        curl \
#        libreoffice \
#        tzdata \
#        python3-pip && \
#    ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
#    apt-get clean && \
#    rm -rf /var/lib/apt/lists/*
RUN apk update && \
    apk add --no-cache \
        curl \
        libreoffice \
        tzdata \
        py3-pip && \
    ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    rm -rf /var/cache/apk/* /tmp/* /var/tmp/*

## 安装语言包
#RUN for LOCALE in $(curl -sL https://raw.githubusercontent.com/thelamer/lang-stash/master/langs); do \
#      apt-get install -y --no-install-recommends libreoffice-lang-$(echo ${LOCALE}| tr '[:upper:]' '[:lower:]') || apt-get install -y --no-install-recommends libreoffice-lang-$(echo ${LOCALE}| head -c2); \
#    done && \
#    apt-get clean && \
#    rm -rf /var/lib/apt/lists/*

# 安装字体
# alpine: https://wiki.alpinelinux.org/wiki/Fonts
# debign: https://wiki.debian.org/Fonts
RUN apk add --no-cache \
    font-noto font-noto-cjk font-noto-extra \
    terminus-font \
    ttf-font-awesome \
    ttf-dejavu \
    ttf-freefont \
    ttf-hack \
    ttf-inconsolata \
    ttf-liberation \
    ttf-mononoki  \
    ttf-opensans   \
    fontconfig && \
    fc-cache -f

# 安装unoconvert.go
# https://github.com/unoconv/unoserver#installation
RUN pip3 install --no-cache unoserver==3.0.1 --break-system-packages

# 验证 LibreOffice 和 unoconvert 版本
RUN libreoffice --headless --version
RUN unoserver -v
