FROM mcr.microsoft.com/devcontainers/base:bookworm

ARG USER=vscode
ARG USER_ID=1000
ARG GROUP_ID=1000

RUN apt-get update -y \
    && DEBIAN_FRONTEND=noninteractive apt-get upgrade -y \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    gnupg \
    lsb-release \
    python3.11-venv \
    expect \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/cache/apt/* /var/lib/apt/lists/

RUN if ! getent group $GROUP_ID > /dev/null 2>&1; then groupadd -g $GROUP_ID mygroup; fi
RUN if ! getent passwd $USER_ID > /dev/null 2>&1; then useradd -m -u $USER_ID -g $GROUP_ID $USER; fi

USER $USER_ID
RUN python3 -m venv ~/.venv/myenv \
    && echo "source ~/.venv/myenv/bin/activate" >> ~/.bashrc \
    && /bin/bash -c "source ~/.venv/myenv/bin/activate; pip install --upgrade pip; pip install jupyterlab matplotlib; ipython kernel install --user --name=myenv"
