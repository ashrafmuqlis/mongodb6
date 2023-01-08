# mongodb6
Notes on MongoDB 6.0.3 stacked on Ubuntu 22.04. How to's, etc.

## Copy gpg key for mongodb 6.0.3
```
wget -q -O - https://www.mongodb.org/static/pgp/server-6.0.pub | sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/mongodb.gpg
```

```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list
```

## Update APT with 3rd party repo

```
sudo apt update
```

## Install and configure mongodb community edition
```
sudo apt install mongodb-org
```

```
sudo systemctl start mongod.service
```

```
sudo systemctl status mongod
```

```
sudo systemctl enable mongod
```

```
mongosh
```

```
cat /etc/mongod.conf
```

--------------
ENABLE REMOTE ACCESS (Localhost and Machine IP)
--------------
```
#!bin/bash

file1="127.0.0.1"
file2=`hostname -I | xargs`

echo $file1, $file2

echo "sudo sed -ie '21 s/"$file1/$file1, $file2"/' /etc/mongod.conf" > mongo_remote.sh

bash ./mongo_remote.sh

sudo systemctl restart mongod.service
```

--------------
ENABLE DEFAULT ACCESS (Localhost only)
--------------
```
#!bin/bash

file1="127.0.0.1"
file2=`hostname -I | xargs`

echo $file1, $file2

echo "sudo sed -ie '21 s/"$file1, $file2/$file1"/' /etc/mongod.conf" > mongo_default.sh

bash ./mongo_default.sh

sudo systemctl restart mongod.service
```
