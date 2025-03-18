ARG UV_VERSION=latest
ARG DEBIAN_VERSION=bookworm

FROM ghcr.io/astral-sh/uv:$UV_VERSION AS uv

FROM mcr.microsoft.com/vscode/devcontainers/base:$DEBIAN_VERSION

LABEL maintainer="trymzet <mzawadzki@dyvenia.com>"

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install DuckDB CLI.
RUN curl https://install.duckdb.org | sh
RUN mv ${HOME}/.duckdb/cli/latest/duckdb /bin/duckdb && \
    chown vscode: /bin/duckdb

COPY --from=uv --chown=vscode: /uv /uvx /bin/

ENV DISPLAY=dummy
ENV PYTHONUNBUFFERED=True
ENV UV_LINK_MODE=copy
ENV UV_COMPILE_BYTECODE=True
