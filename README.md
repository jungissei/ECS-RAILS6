# SET UP

```
$ git clone https://github.com/jungissei/ECS-RAILS6
$ cd ECS-RAILS6
$ docker-compose run app rails new . --force --database=mysql
$ vi config/database.yml
```


- daatabase.ymlの編集
```
default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: <%= ENV['MYSQL_ROOT_PASSWORD'] %>
  host: <%= ENV['MYSQL_HOST'] %>

development:
  <<: *default
  database: app_development

test:
  <<: *default
  database: app_test

production:
  <<: *default
  database: <%= ENV['DB_DATABASE'] %>
  adapter: mysql2
  encoding: utf8mb4
  charset: utf8mb4
  collation: utf8mb4_general_ci
  host: <%= ENV['DB_HOST'] %>
  username: <%= ENV['DB_USERNAME'] %>
  password: <%= ENV['DB_PASSWORD'] %>


```


```
$ vi config/environments/development.rb
```



```development.rb
Rails.application.configure do
  config.hosts.clear #追加
```

- production.rb
```
config.eager_load = false #true→false

#ENV['RAILS_SERVE_STATIC_FILES'].present?→true
# config.public_file_server.enabled = ENV['RAILS_SERVE_STATIC_FILES'].present?
config.public_file_server.enabled = true

```



```
$ cp docker/rails/puma.rb config/ (pumaの設定を上書き)
$ mkdir -p tmp/sockets  (socketファイルの置き場所を確保)
$ docker-compose up -d --build
$ docker-compose run app rails db:create
```



