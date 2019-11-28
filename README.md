# docker-spark-livy-python3
A sample Dockerfile for Apache Spark working with Apache Livy and additional version of Python interpreter

## Usage

### 1. clone repository

```sh
git clone https://github.com/Yuhsak/docker-spark-livy-python3.git
cd docker-spark-livy-python3/spark
```

### 2. Build image

**with docker-compose**

```sh
docker-compose build
```

**without docker-compose**

```sh
docker build -t spark-livy:2.4.4 .
```

### 3. Run containers

**with docker-compose**

```sh
docker-compose up
# Or specify scaling number against worker containers
docker-compose up --scale worker=3
```

**without docker-compose**

```sh
# Create network
docker network create spark
# Start master
docker run -itd --net=spark -p 7077:7077 -p 8080:8080 -p 8998:8998 --name spark-master spark-livy:2.4.4 bash -c "/livy/bin/livy-server start && /spark/bin/spark-class org.apache.spark.deploy.master.Master --host 0.0.0.0"
# Start worker
docker run -itd --net=spark -p 8081:8081 --name spark-worker spark-livy:2.4.4 /spark/bin/spark-class org.apache.spark.deploy.worker.Worker spark://spark-master:7077 --host 0.0.0.0
```


### 4. Open WebUI to realize that your spark cluster working

Spark WebUI

```sh
open http://localhost:8080
```

Livy UI
```sh
open http://localhost:8998
```
