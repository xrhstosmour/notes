#docker #docker-context #ssh #remote

Instead of `ssh`-ing in to run `docker`/`docker-compose` commands (see [[Deploy via SSH]] for that flow), point the local Docker CLI at a remote daemon over SSH:

```
docker context create <context_name> --docker "host=ssh://<user>@<host>:<port>"
docker context use <context_name>
```

Every subsequent `docker`/`docker compose` command now runs against the remote host transparently, `docker ps`, `docker compose up -d`, etc. all target it, no explicit SSH session needed once the context is set. Switch back to the local daemon with `docker context use default`.
