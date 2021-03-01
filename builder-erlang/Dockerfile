FROM erlang:22

RUN apt update
RUN apt-get install -y -q \
        build-essential \
        bison \
        flex \
        git \
        gzip \
        autotools-dev \
        automake \
        libtool \
        pkg-config \
        cmake \
        libsodium-dev

ENV PATH="/root/.cargo/bin:${PATH}"
RUN curl https://sh.rustup.rs -sSf | sh -s -- -y --default-toolchain stable
RUN rustup update