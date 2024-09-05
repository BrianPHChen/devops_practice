### Assignment
* Use the Drupal compose file from `compose-assignment-2`
* Rename image back to drupal:8.2
* Remove `build:`
* Add secret via `external:`
* use enviroment var `POSTGRES_PASSWORD_FILE`
* Add secret via cli `echo "<pw>" | docker secret create psql-pw -`
* Copy compose into a new yml file on Swarm node 1

### Answer
* Goto `swarm-secrets-assignment-1`

> docker stack deploy -c docker-compose.yml drupal

會出現 secret not found: psql-pw, 所以都要先create secret

> echo "<string>" | docker secret create psql-pw -

然後就可以在用上面那個指令deploy stack