# rails環境のフルセット構成の




# 参考

Ruby on Rails install
http://qiita.com/saito400/items/c7e83db54f2fdc9d145a
http://qiita.com/oshin/items/0d011610238eb4df83fd
http://blog.yuuk.io/entry/large-scale-infrastructure


http://qiita.com/osamtimizer/items/3a241f365c85356394a8

minio
http://enakai00.hatenablog.com/entry/2015/07/16/173015


# rails-cluster docker-compose の使い方
docker-compose pull
docker-compose up -d

docker-compose down
docker-compose down --remove-orphan


# プロジェクトの開始
    $ cd <プロジェクト開始フォルダ>
    $ bundle init
      Gemfileが出来上がるので編集
    $ bundle install --path vendor/bundle
    $ bundle exec rails new .
      Gemfile上書きでOK

# プロジェクトの実行
    $ cd <app>
    $ bundle exec rails server -p 3000 -b '0.0.0.0'


# ディレクトリ構成
rails_app
rails_db
rails_redis
rails_worker
