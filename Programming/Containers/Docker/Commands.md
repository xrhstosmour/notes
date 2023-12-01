#docker #containers #commands
- Copy data from container: ```docker cp <container_id>:/container/path /host/save/location```
- Export image as tar: ```docker save <image_id> -o /save/location/image.tar```
- Load image from tar: ```docker load -i /save/location/image.tar```
- Remove dangling images: ```docker image prune --filter="dangling=true"```
- Delete all log files: ```sudo sh -c "truncate -s 0 /var/lib/docker/containers/*/*-json.log"```
- Rename volumes: ```docker volume create --name <new_volume> && docker run --rm -it -v <old_volume>:/from -v <new_volume>:/to alpine ash -c 'cd /from ; cp -av . /to' && docker volume rm <old_volume>```
