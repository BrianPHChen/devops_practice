### Using secrets with local docker compose
如果沒有用swarm 用compose執行上面的指令

> docker-compose exec psql cat /run/secrets/psql_user

沒有database所以會直接噴value出來

雖然不安全，但至少你可以用local compose 模擬swarm狀況

### App 

* 參考`swarm-stack-3` 有一個基礎的composefile, 然後讓其他的overwrite

> $ docker-compose up -d

* override會被自動combine 如果是自定義的override則要加上`-f`

> docker-compose -f docker-compose.yml -f docker-compose.test.yml up -d

* 可以看最後加上config來看長什麼樣子

> docker-compose -f docker-compose.yml -f docker-compose.prod.yml config