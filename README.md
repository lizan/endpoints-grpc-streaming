# Endpoints GRPC streaming example

Using [routeguide service from GRPC examples](http://www.grpc.io/docs/tutorials/basic/go.html).

### Combining multiple GRPC services into a single service config

Replace SERVICE_NAME to real one in [`api_config.yaml`](./api_config.yaml).

```
$ protoc --include_imports --include_source_info route_guide.proto --descriptor_set_out=out.pb

$ gcloud beta service-management deploy out.pb api_config.yaml
```

Get service-name and config-id from the command output.

### Deploy to Kubernetes

Replace SERVICE_NAME and SERVICE_CONFIG_ID to real one in [`grpc-routeguide.yaml`](./grpc-routeguide.yaml).
```
$ kubectl create -f grpc-routeguide.yaml
```

### Using client from examples

Install go route guide client
```
mkdir /tmp/go
export GOPATH=/tmp/go
go get google.golang.org/grpc/examples/route_guide/client
```

Get kubernetes service-ip
```
kubectl get svc/esp-grpc-routeguide
```

Run client
```
$GOPATH/bin/client -server_addr <YOUR-SERVICE-IP>:80
```
