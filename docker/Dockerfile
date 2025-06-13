# Ubuntu系linux環境用
FROM ubuntu:latest

ARG DEBIAN_FRONTEND=noninteractive

# 基本ユーティリティのインストール
RUN echo "==> Installing system utilities..." && \
    apt-get update && \
    apt-get install -y wget sudo dos2unix jq

# Python3 と pip のインストール
RUN echo "==> Installing Python3 and pip..." && \
    apt-get install -y python3 python3-pip

# LangChain 関連ライブラリのインストール
RUN echo "==> Installing LangChain and related packages..." && \
    pip install --break-system-packages -U --quiet langchain_experimental langchain langchain-community && \
    pip install --break-system-packages chromadb && \
    pip install --break-system-packages tiktoken

# Streamlit のインストール
RUN echo "==> Installing Streamlit..." && \
    pip install --break-system-packages --upgrade streamlit

# tshark（Wireshark CLI）のインストール
RUN echo "==> Installing tshark..." && \
    apt-get install -y tshark

# PyShark のインストール
RUN echo "==> Installing PyShark..." && \
    pip install --break-system-packages pyshark

# その他 Python パッケージ
RUN echo "==> Installing additional Python packages..." && \
    pip install --break-system-packages requests && \
    pip install --break-system-packages -U sentence-transformers==2.2.2 && \
    pip install --break-system-packages InstructorEmbedding

# スクリプトとコードのコピー
COPY /packet_buddy /packet_buddy/
COPY /scripts /scripts/

# スクリプトの改行コード変換
RUN echo "==> Converting script line endings..." && \
    dos2unix /scripts/startup.sh

# 起動コマンド
CMD ["/bin/bash", "/scripts/startup.sh"]
