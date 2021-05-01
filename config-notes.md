### docker config
https://stackoverflow.com/questions/65361083/docker-build-failed-to-fetch-oauth-token-for-openjdk

```
export DOCKER_BUILDKIT=0
export COMPOSE_DOCKER_CLI_BUILD=0
```

### docker commands
- docker build -t react-app .
- docker build -t react-appaustin2153/react-app

### misc
- docker exec -it CONTAINER_NAME sh #run shell in container
- docker start CONTAINER #starts a stopped container
- docker container prune #get rid of all stopped containers
- docker image tag 879afb330dc0 austin2153/react-app:1.0.0 #tag an existing image with a tag
- docker exec -it d8ff sh

### volumes
- docker volume create app-data
- docker volume inspect app-data

    ```
    This mount exists on the mobylinux VM running docker in WSL1

    [
        {
            "CreatedAt": "2021-04-30T00:08:02Z",
            "Driver": "local",
            "Labels": {},
            "Mountpoint": "/var/lib/docker/volumes/app-data/_data",
            "Name": "app-data",
            "Options": {},
            "Scope": "local"
        }
    ]
    ```

### docker run
- docker run -it react-app sh | *run shell inside interactive container session* | 
- docker run react-app ||
- docker run -d react-app *-d is detached mode* |
- docker run -d -p 4000:3000 -v app-data:/app/data react-app *map 4000 from localhost and mount - volume app-data to /app/data*
- docker run -d -p 5000:3000 -v app-data:/app/data react-app
- docker run -d -p 5000:3000 --mount source=app-data,target=/app/data react-app

### docker cp
- docker cp CONTAINER:FULLPATH LOCALDIRECTORY *Copy a file from container to host*
- docker cp 6d128bc46daf:/app/log.txt .
- docker cp secret.txt 6d128bc46daf:/app *Copy file from host to container*

### sharing source with container
- docker run -d -p 5000:3000 -v $(pwd):/app -v app-data:/app/data react-app
- docker run -p 5000:3000 -v $(pwd):/app react-app
- docker run -v /mnt/c/Users/acampbell/wsl/dev/voltest:/app voltest

    ```
    npm ERR! code ENOENT
    npm ERR! syscall open
    npm ERR! path /app/package.json
    npm ERR! errno -2
    npm ERR! enoent ENOENT: no such file or directory, open '/app/package.json'
    npm ERR! enoent This is related to npm not being able to find a file.
    npm ERR! enoent

    npm ERR! A complete log of this run can be found in:
    npm ERR!     /home/app/.npm/_logs/2021-04-30T01_37_36_851Z-debug.log
    ```
    ```
    api_1  | npm ERR! code ENOENT
    api_1  | npm ERR! syscall open
    api_1  | npm ERR! path /app/package.json
    api_1  | npm ERR! errno -2
    api_1  | npm ERR! enoent ENOENT: no such file or directory, open '/app/package.json'
    api_1  | npm ERR! enoent This is related to npm not being able to find a file.
    api_1  | npm ERR! enoent
    api_1  |
    api_1  | npm ERR! A complete log of this run can be found in:
    api_1  | npm ERR!     /home/app/.npm/_logs/2021-04-30T20_01_38_088Z-debug.log
    vidley_api_1 exited with code 254
    ```
enoent ENOENT: no such file or directory enoent This is related to npm not being able to find a file

### docker logs
- docker logs -f 7d8d *see the changes as the container is started*

### clean up images and containers
- docker image prune
- docker container prune

### login with root user
docker exec -it -u root a13ef sh