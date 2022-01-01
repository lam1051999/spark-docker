# Declare framework version

```sh
SPARK_VERSION="3.2.0"
HADOOP_VERSION="3.2"
JUPYTERLAB_VERSION="3.2.5"
```

# Build images

Build base image

```sh
docker build \
  --platform=linux/arm64 \
  -f cluster_base/Dockerfile \
  -t spark-cluster-base .
```

Build Spark base image

```sh
docker build \
  --build-arg spark_version="${SPARK_VERSION}" \
  --build-arg hadoop_version="${HADOOP_VERSION}" \
  -f spark_base/Dockerfile \
  -t spark-base .
```

Build Spark master image

```sh
docker build \
  -f master_node/Dockerfile \
  -t spark-master .
```

Build Spark worker image

```sh
docker build \
  -f worker_node/Dockerfile \
  -t spark-worker .
```

Build Jupyterlab image

```sh
docker build \
  --build-arg spark_version="${SPARK_VERSION}" \
  --build-arg jupyterlab_version="${JUPYTERLAB_VERSION}" \
  -f jupyter_lab/Dockerfile \
  -t spark-jupyterlab .
```