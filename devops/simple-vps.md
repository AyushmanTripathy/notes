# Simple VPS

- Following tools are being used
    1. Docker & Docker Swarm
    2. Git bare repo & `post-receive` hook
    3. Caddy & redis as a systemd service

## Build and Deployment

- We will trigger deployment using `git push prod main` 
- prod is a bare repository in our VPS.
- We use docker swarm for rolling deployment

```sh
git --work-dir=$WORK_DIR --git-dir=$GIT_DIR checkout -f main
cd $WORK_DIR

COMMIT=%(git rev-parse --short HEAD)
docker build -t app:$COMMIT app:latest .
docker stack deploy
```

## Logging

- Using docker built in logs
- Logs for `post-receive` hook is redirected to a file.

```
docker stack services <stack_name>
docker events
```

## Routing

- Using globally installed Caddy

```
app1.example.com {
    reverse_proxy localhost:8080
}

app2.example.com {
    reverse_proxy localhost:8081
}
```
