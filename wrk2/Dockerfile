FROM ubuntu:18.04

RUN rm /etc/apt/sources.list
COPY ./sources.list /etc/apt/sources.list

COPY /usr/lib64/libcrypto.so.1.0.2k /lib/x86_64-linux-gnu/
COPY /usr/lib64/libssl.so.1.0.2k /lib/x86_64-linux-gnu/
RUN cd /lib/x86_64-linux-gnu/ && ln -sf libssl.so.1.0.2k libssl.so.10 && ln -sf libcrypto.so.1.0.2k libcrypto.so.10

RUN apt-get update -y
RUN apt -y install libgssapi-krb5-2
# RUN apt-get install luarocks -y
# RUN luarocks install luasocket

WORKDIR /root
COPY ./wrk2 /bin/wrk2

# 除此以外，需要包含三个基准测试的lua脚本文件
COPY ./hotel_lua ./hotel_lua
COPY ./social_lua ./social_lua
COPY ./media_lua ./media_lua

ENTRYPOINT ["/bin/wrk2"]