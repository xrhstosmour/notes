#docker #docker-compose #deploy #ssh

A minimal SSH-based deploy for a `docker-compose` project, no CI/CD pipeline required:

1. Copy the deploy artifact (a tarball of the project) to the remote host:
```
scp -i <path_to_key> -P <port> <artifact>.tar.gz <user>@<host>:<remote_path>
```
2. Connect and extract:
```
ssh -i <path_to_key> -p <port> <user>@<host>
cd <remote_path>
tar -xzf <artifact>.tar.gz
```
3. Bring the stack up:
```
docker-compose up -d
```
