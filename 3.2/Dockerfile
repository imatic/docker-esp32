FROM debian:stretch

ENV ESP_IDF_VERSION="v3.2" IDF_PATH="/opt/esp-idf" PATH="/opt/xtensa-esp32-elf/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"

RUN apt-get update && \
    apt-get install --yes curl make gnupg && \
    echo "deb http://apt.llvm.org/stretch/ llvm-toolchain-stretch-7 main" >> /etc/apt/sources.list && \
    curl --no-buffer --silent https://apt.llvm.org/llvm-snapshot.gpg.key | apt-key add - && \
    apt-get update && \
    apt-get install --yes clang-format-7 gcc git make libncurses-dev flex bison gperf python python-pip python-setuptools python-serial python-cryptography python-future && \
    ln -s $(which clang-format-7) /usr/local/bin/clang-format && \
    curl -o xtensa-exp32-elf.tar.gz https://dl.espressif.com/dl/xtensa-esp32-elf-linux64-1.22.0-80-g6c4433a-5.2.0.tar.gz && \
    tar -C /opt -xvzf ./xtensa-exp32-elf.tar.gz && \
    git clone --depth 1 --branch ${ESP_IDF_VERSION} --recursive https://github.com/espressif/esp-idf.git /opt/esp-idf && \
    python -m pip install --user -r $IDF_PATH/requirements.txt && \
    apt-get remove --yes gnupg curl && \
    apt-get autoremove --yes && \
    rm -rf /var/lib/apt/lists/*
