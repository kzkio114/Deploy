# ベースイメージの指定
# macのOSバージョンアップ(14.3.1)したら--platform=linux/amd64でエラーでるようになった？
FROM --platform=linux/amd64 ruby:3.2.2

# 必要なパッケージのインストール
RUN apt-get update -qq && apt-get install -y build-essential default-mysql-client

# 作業ディレクトリの設定
WORKDIR /api

# GemfileとGemfile.lockをコンテナ内にコピー
COPY Gemfile /api/Gemfile
COPY Gemfile.lock /api/Gemfile.lock

# Bundlerを使ってRuby gemsをインストール
RUN bundle install

# ホストのファイルをコンテナ内の作業ディレクトリにコピー
COPY . /api

# スタートアップスクリプトをコンテナ内にコピーし、実行権限を設定
COPY start.sh /start.sh
RUN chmod 744 /start.sh

# コンテナ起動時に実行されるコマンド
CMD ["sh", "/start.sh"]