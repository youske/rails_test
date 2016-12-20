
# 参考

Ruby on Rails install
http://qiita.com/saito400/items/c7e83db54f2fdc9d145a


http://qiita.com/oshin/items/0d011610238eb4df83fd


http://blog.yuuk.io/entry/large-scale-infrastructure


http://qiita.com/osamtimizer/items/3a241f365c85356394a8


# プロジェクトの開始
$ cd <プロジェクト開始フォルダ>
$ bundle init
  Gemfileが出来上がるので編集
$ bundle install --path vendor/bundle
$ bundle exec rails new .


# ディレクトリ構成
rails_app
rails_db
rails_redis
rails_worker
