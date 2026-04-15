FROM mcr.microsoft.com/devcontainers/base:ubuntu-24.04

ENV http_proxy http://perceval.orange.com.do:8080
ENV https_proxy http://perceval.orange.com.do:8080

COPY --from=jdxcode/mise /usr/local/bin/mise /usr/local/bin/

ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update && apt-get install -y --no-install-recommends \
  git curl ca-certificates sudo zsh \
  && rm -rf /var/lib/apt/lists/* \
  && usermod -s /usr/bin/zsh vscode

RUN if command -v mise >/dev/null 2>&1; then \
  mise install chezmoi || true; \
  else \
  curl -sfL https://get.chezmoi.io | sh -s -- -b /usr/local/bin || true; \
  fi



RUN echo 'eval "$(mise activate bash)"' >> /etc/skel/.bashrc && \
  echo 'eval "$(mise activate zsh)"' >> /etc/skel/.zshrc
