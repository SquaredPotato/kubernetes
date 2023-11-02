# immich-secret.sops.yaml layout
```yaml
apiVersion: v1
kind: Secret
metadata:
    name: immich
    namespace: immich
type: Opaque
stringData:
    REDIS_URL: ioredis://<place base64 encoded json here>
```

Here, `REDIS_URL` should be set to a base64 encoded version of a filled-in version of the following JSON:
```JSON
{
    "db": 1,
    "password": "<redis_password_here>",
    "sentinels": [
        {
            "host": "ioredis://redis-node-0.redis-headless.database.svc.cluster.local",
            "port": 26379
        },
        {
            "host": "ioredis://redis-node-1.redis-headless.database.svc.cluster.local",
            "port": 26379
        },
        {
            "host": "ioredis://redis-node-2.redis-headless.database.svc.cluster.local",
            "port": 26379
        }
    ],
    "sentinelPassword": "<redis_password_here>",
    "name": "redis-master"
}
```
Before encoding, remove all enters and spaces.

**Do not forget to encrypt the created file**

