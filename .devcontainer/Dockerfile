FROM ubuntu:22.04

RUN apt update && apt install -y \
    git \
    curl \
    vim \
    htop \
    jq \
    make \
    nasm \
    build-essential \
    qemu \
    qemu-system-x86

RUN curl -Ls https://deb.nodesource.com/setup_18.x | bash
RUN apt update && apt install -y nodejs

RUN useradd -m user

CMD [ "sleep", "infinity" ]
