# starlab-helm-charts

## Puddle
Puddle is STARLAKE's development playground to validate data streams/transformations, test out k8s deployments and new technologies for STARLAKE's data stack.

### 1. Installing Kafka
```
helm upgrade kafka ./kafka-minimal --install --atomic -n starlake-kafka --create-namespace \
--set image=confluentinc/cp-kafka:7.4.1 \
--set storageClass=crc-csi-hostpath-provisioner
```

### 2. Installing Schema Registry
```
helm upgrade schemaregistry ./schemaregistry-minimal --install --atomic -n starlake-kafka --create-namespace \
--set image=confluentinc/cp-schema-registry:7.4.1
```

### 3. Installing Kafka Connect
```
helm upgrade kafka-connect ./kafka-connect-ss-minimal --install --atomic -n starlake-kafka --create-namespace \
--set image=llzd98/cp-kafka-connect-custom:7.4.1 \
--set replicas=1 \
--set route.tls.enabled=true
```
### 4. Installing ksqlDB 
```
helm upgrade kafka-ksqldb-server ./kafka-ksqldb-server --install -n starlake-kafka --atomic
```
### 5. Installing AKHQ (Admin UI page)

```
helm upgrade akhq ./akhq-minimal --install --atomic -n starlake-kafka --create-namespace \
--set image=tchiotludo/akhq:0.24.0 \
--set passwordSha256=9a83572fcd4d8606bd0298c5fdd9807d8e5a8b09ab67ac89f76d842fa38346f6
```
To convert pw to sha25, use `echo -n 'plschangeme' | sha256sum`

### 6. Installing Postgres DB
```
helm upgrade postgres ./postgres-minimal --create-namespace --install --atomic \
--namespace starlake-kafka \
--set storageClass=crc-csi-hostpath-provisioner \
--set image=bitnami/postgresql:16.1.0-debian-11-r0
```
default credentials are:

host: `svc-postgres-headless`

user: `postgres-db`

password: `plschangeme`

### 7. Installing PgAdmin (Optional)
```
helm upgrade pgadmin ./pgadmin-minimal -n starlake-kafka --create-namespace --install --atomic \
--set storageClass=crc-csi-hostpath-provisioner \
--set route.tls.enabled=true
```
Default credentials are:

email: `pgadm@test.net`

password: `plschangeme`

### 8. Create data generator deployment

### 9. Source Connector

### 10. Sink Connector