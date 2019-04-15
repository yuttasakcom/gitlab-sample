# Gitlab Sample

## Gen cert, key

```

```

## Register Gitlab-Runner

```bash
docker-compose exec gitlab-runner gitlab-runner register -n --tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token hJzbDkKcfHWzQ7-A1htN --description "my-runner" --tag-list build --executor docker --docker-image "docker:latest" --docker-privileged

docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token hJzbDkKcfHWzQ7-A1htN --description "docker" --tag-list docker --executor docker --docker-image "docker:stable" --docker-privileged --run-untagged --locked="false"


docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token zMERh-1Vp3AMFU13QG5y --description "docker" --tag-list docker --executor docker --docker-image "docker:stable" --docker-volumes /etc/hosts:/etc/hosts --docker-volumes /var/run/docker.sock:/var/run/docker.sock --docker-volumes /etc/gitlab-runner/certs/ca.crt:/etc/gitlab-runner/certs/ca.crt
```

## Copy ssl from gitlab-ce

```bash
docker cp 2854c1ea8c86:/etc/gitlab/ssl/gitlab.example.com.crt .
docker cp 2854c1ea8c86:/etc/gitlab/ssl/gitlab.example.com.key .
```

## Options gitlab-ce

```
nginx['ssl_protocols'] = "TLSv1 TLSv1.1 TLSv1.2"
nginx['redirect_http_to_https'] = true
nginx['listen_port'] = 443
gitlab_rails['time_zone'] = 'Asia/Bangkok'
```
