# .devcontainer/Dockerfile

# --- ベースイメージの選択 ---
# Microsoftが提供する公式のDev Containerイメージを使用するのがベストプラクティスです。
# "mcr.microsoft.com/devcontainers/universal:latest" は
# Node, Python, Java, Goなど、主要な言語のランタイムとツールがあらかじめ含まれており、
# ほとんどの開発ニーズに対応できます。
FROM mcr.microsoft.com/devcontainers/universal:latest

# --- 環境設定とパッケージの追加 ---
# rootユーザーで追加のパッケージをインストールします。

# apt-get updateの実行
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    # 開発に必要な追加のシステムパッケージをインストールします。
    # 例: SQLiteの開発ファイル (多くのPythonプロジェクトで使用される)
    && apt-get -y install --no-install-recommends \
        sqlite3 \
        libsqlite3-dev \
    # 不要になったaptキャッシュをクリーンアップし、イメージサイズを小さく保ちます。
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# --- ユーザー設定 ---
# Dev Containerのベストプラクティスとして、rootではなく非特権ユーザー(vscode)で開発を行うべきです。
# universalイメージでは 'vscode' ユーザーが既に存在します。
USER vscode

# --- ツール設定 (非rootユーザー) ---
# このセクションで、非rootユーザーとして言語ごとのツールを設定します。

# npmのグローバルパッケージをインストール (例: TypeScriptの言語サーバー、CLIツール)
RUN npm install -g typescript ts-node

# Pythonのパッケージをインストール (例: コードフォーマッター、リンター)
# universalイメージにはpipがすでに含まれています。
RUN pip install black flake8

# --- 終了 ---
# これで、Node.jsとPythonの両方をサポートする、再現性の高い開発環境が完成しました。
