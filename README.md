# docker-spark-livy-python3
A sample Dockerfile for Apache Spark working with Apache Livy and additional version of Python interpreter

## Usage

1. clone repository

```sh
git clone https://github.com/Yuhsak/docker-spark-livy-python3.git
``

2. Build image & Run container

```sh
cd docker-spark-livy-python3/spark
docker-compose up
# Or specify scaling number against worker containers
docker-compose up --scale worker=3
```

3. Open WebUI to realize that your spark cluster working

Spark WebUI

```sh
open http://localhost:8080
```

Livy UI
```sh
open http://localhost:8998
```