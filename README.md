# Quickstart: gRPC
Run grpc/examples/python/helloworld python greeter_server.py &amp; greeter_client.py on two virtual machines.

## Docker pull
```
docker pull tensorflow/tensorflow:2.2.0-gpu
```

## Greeter server
Running Container
```
docker run --gpus all --name grpc-server -v ./gRPC/server:/media -itd tensorflow/tensorflow:2.2.0-gpu
```

Show running containers and run a command in a running container
```
docker ps
docker exec -it [CONTAINER ID] /bin/bash
```

Install git and grpc
```
apt-get install git
python -m pip install --upgrade pip
python -m pip install grpcio
python -m pip install grpcio-tools
```

Clone the repository to get the example code
```
cd media
git clone -b v1.28.1 https://github.com/grpc/grpc
cd grpc/examples/python/helloworld
```

Run greeter_server.py
```
python greeter_server.py
```

## Greeter client
Running Container
```
sudo docker run --gpus all --name grpc-client -v ./gRPC/client:/media -itd tensorflow/tensorflow:2.2.0-gpu
```

Repeat the `Show running containers and run a command in a running container`, `Install git and grpc` and `Clone the repository to get the example code`

```
sudo chown -R swpc ./gRPC/client/grpc
```

Open `./gRPC/client/grpc/examples/python/helloworld/greeter_client.py`

Check container ip
```
docker network inspect bridge
```

Change **with grpc.insecure_channel`('localhost:50051')` as channel:** into **`('172.17.0.2:50051')`**

Run greeter_client.py
```
python greeter_client.py
```

**Then you will see "Greeter client received: Hello, you!"**
