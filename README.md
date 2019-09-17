## Build s2i image

```
docker build -t shapeblock/rails:2.6 .
docker push shapeblock/rails:2.6
```

## Build nginx image

```
docker build -t shapeblock/nginx-rails:1.17 .
docker push shapeblock/nginx-rails:1.17
```

## Import into OpenShift

```
oc import-image shapeblock/rails:2.6 --confirm -n openshift
oc import-image shapeblock/nginx-rails:1.17 --confirm
```
