# MONGODB-K8s

## Simple Mongodb deployment in kubernetes cluster

### Objects:

```bash
- Mongodb deployment manifest
- Mongodb service manifest
- Mongodb secret manifest
- Mongo-express deployment manifest
- Mongo-express service manifest
- Mongo-express configmap manifest
```

### Breakdown:

```bash
mongo.yaml # Deployment file. 1 replica, image: mongo4.4, environment variables set from secret. Container port: 27017

mongo-service.yaml # Service manifest. Port & target port 27017. Type clusterIP.

mongodb-secret.yaml # Secret manifest. Referenced in deployment manifest. Defines value for required db environment variables. base64 encoded placeholders

mongo-express.yaml # Deployment manifest. 1 replica, image: mongo-express, environment variables pulled from mongodb-secret, datbase url pulled from mongodb-configmap

mongo-express-service.yaml # Service manifest. NodePort service to expose mongo-express externally. Port & target port 8081.

mongo-express-configmap.yaml # Configmap referenced by mongo-express deployment. Contains database URL env variable.
```

### IMPLEMENTATION:

1. Use BASE64 to encode a username and password and set them inside of the secret manifest. `echo -n <username> | base64 && echo -n <password> | base64`
2. Run `kubectl apply -f .` This will create the objects in the required order for everything to function properly.
