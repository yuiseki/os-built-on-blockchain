FROM ubuntu:22.04

RUN apt update && apt install -y \
    git \
    curl \
    wget \
    vim \
    htop \
    jq \
    make \
    build-essential \
    # qemu
    qemu \
    qemu-system-x86 \
    # asm
    nasm \
    # Linux kernel
    bc ncurses-dev bison flex libelf-dev openssl libssl-dev \
    # busybox
    cpio

RUN curl -Ls https://deb.nodesource.com/setup_18.x | bash
RUN apt update && apt install -y nodejs

RUN useradd -m user

CMD [ "sleep", "infinity" ]
