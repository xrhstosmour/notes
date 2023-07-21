#docker #containers #commands
- Copy data from container: ```docker cp <container_id>:/container/path /host/save/location```
- Export image as tar: ```docker save <image_id> -o /save/location/image.tar```
- Load image from tar: ```docker load -i /save/location/image.tar```
- Remove dangling images: ```docker image prune --filter="dangling=true"```
