# How to run mongodb with replication and keyfile authentication in pterodactyl
Use the [MongoDB 8 egg](https://github.com/Ptero-Eggs/application-eggs/blob/main/database/nosql/mongodb/egg-mongo-d-b8.json)

1. Make a server. Make sure start server after install is disabled
2. Change the server or the egg's startup command to
```sh
rm -f /home/container/mongo-keyfile && cat /home/container/source-keyfile > /home/container/mongo-keyfile && chmod 400 /home/container/mongo-keyfile && ls -l /home/container/mongo-keyfile && mongod --fork --dbpath /home/container/mongodb/ --port ${SERVER_PORT} --bind_ip 0.0.0.0 --logpath /home/container/logs/mongo.log -f /home/container/mongod.conf; until nc -z -v -w5 127.0.0.1 ${SERVER_PORT}; do echo 'Waiting for mongodb connection...'; sleep 5; done; mongosh "mongodb://${MONGO_USER}:${MONGO_USER_PASS}@127.0.0.1:${SERVER_PORT}/admin" && mongosh "mongodb://${MONGO_USER}:${MONGO_USER_PASS}@127.0.0.1:${SERVER_PORT}/admin" --eval "db.getSiblingDB('admin').shutdownServer()"
```
4. Create source-keyfile in /home/container with your keyfile
5. In mongod.conf set
```yml
security: 
  keyFile: /home/container/mongo-keyfile

replication:
  replSet: "rs0"
```
5. Start the server
