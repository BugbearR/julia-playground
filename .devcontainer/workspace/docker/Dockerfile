FROM mcr.microsoft.com/devcontainers/base:bullseye

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
    python3-pip \
    expect \
    && apt-get autoremove -y \
    && apt-get clean \
    && rm -rf /var/cache/apt/* /var/lib/apt/lists/

RUN if ! getent group $GROUP_ID > /dev/null 2>&1; then groupadd -g $GROUP_ID mygroup; fi
RUN if ! getent passwd $USER_ID > /dev/null 2>&1; then useradd -m -u $USER_ID -g $GROUP_ID $USER; fi

USER $USER_ID

RUN /usr/bin/python3 -m pip install ipykernel -U --user --force-reinstall
RUN expect -c 'spawn bash -c "curl -fsSL https://install.julialang.org | sh"; expect "Proceed"; send -- "\r"; expect eof'
