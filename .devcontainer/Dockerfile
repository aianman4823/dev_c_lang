# Ubuntuをベースイメージとして使用
FROM ubuntu:22.04

# タイムゾーンの設定を回避
ARG DEBIAN_FRONTEND=noninteractive

# 必要なパッケージのインストール
RUN apt-get update && apt-get install -y \
    build-essential \
    gdb \
    sudo \
    build-essential \
    git \
    iproute2 \
    iputils-ping \
    netcat-openbsd \
    && rm -rf /var/lib/apt/lists/*

# 非rootユーザーを作成
ARG USERNAME=devuser
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# ユーザーとグループを作成
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd --uid $USER_UID --gid $USER_GID -m $USERNAME \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

# ユーザーを切り替え
USER $USERNAME

# ワークディレクトリを設定
WORKDIR /home/$USERNAME

CMD ["/bin/bash"]


