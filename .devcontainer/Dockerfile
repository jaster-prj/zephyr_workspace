FROM debian:latest AS base

RUN apt-get update \
	&& apt-get upgrade -y
RUN apt-get install -y --no-install-recommends git cmake ninja-build gperf \
    ccache dfu-util device-tree-compiler wget \
    python3-dev python3-pip python3-setuptools python3-tk python3-wheel python3-venv xz-utils file \
    make gcc gcc-multilib g++-multilib libsdl2-dev libmagic1

FROM base AS dev

RUN python3 -m venv /opt/venv 

ENV PATH="/opt/venv/bin:$PATH"
	
RUN pip install west

RUN cd /opt && wget https://github.com/zephyrproject-rtos/sdk-ng/releases/download/v0.17.0/zephyr-sdk-0.17.0_linux-x86_64.tar.xz
RUN	cd /opt && tar xvf zephyr-sdk-0.17.0_linux-x86_64.tar.xz
RUN	cd /opt && rm zephyr-sdk-0.17.0_linux-x86_64.tar.xz \
	&& cd zephyr-sdk-0.17.0 \
	&& ./setup.sh -h -t all -c
	
# RUN cp /opt/zephyr-sdk-0.17.0/sysroots/x86_64-pokysdk-linux/usr/share/openocd/contrib/60-openocd.rules /etc/udev/rules.d \
#	&& udevadm control --reload

# ENV GOPATH /go
# ENV PATH $GOPATH/bin:$PATH
# RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 1777 "$GOPATH"

WORKDIR /workspace
