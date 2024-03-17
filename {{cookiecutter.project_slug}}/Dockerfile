FROM ubuntu:latest

WORKDIR /workspace

RUN apt update && \
    apt install -y curl && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

# install rye
ENV RYE_HOME="/opt/rye"
ENV PATH="$RYE_HOME/shims:$PATH"
RUN curl -sSf https://rye-up.com/get | RYE_NO_AUTO_INSTALL=1 RYE_INSTALL_OPTION="--yes" bash

# activate uv
RUN rye config --set-bool behavior.use-uv=true

# rye install the dependencies
COPY pyproject.toml requirements.lock README.md requirements-dev.lock .python-version README.md ./
RUN rye sync
