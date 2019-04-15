# Gitlab Sample

## Gen cert, key

```
openssl req -newkey rsa:2048 -x509 -nodes -keyout ./ssl/gitlab.example.com/gitlab.example.com.key -new -out ./ssl/gitlab.example.com/gitlab.example.com.crt -subj /CN=gitlab.example.com -sha256 -days 365

openssl req -x509 -out ./ssl/gitlab.example.com/gitlab.example.com.crt -keyout ./ssl/gitlab.example.com/gitlab.example.com.key \
 -newkey rsa:2048 -nodes -sha256 \
 -subj '/CN=gitlab.example.com' -extensions EXT -config <( \
 printf "[dn]\nCN=gitlab.example.com\n[req]\ndistinguished_name = dn\n[EXT]\nsubjectAltName=DNS:gitlab.example.com\nkeyUsage=digitalSignature\nextendedKeyUsage=serverAuth")
```

## Register Gitlab-Runner

```bash
docker-compose exec gitlab-runner gitlab-runner register -n --tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token 41KQXM6zCNz8i1nyqn6m --description "my-runner" --tag-list build --executor docker --docker-image "docker:latest"

docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token hJzbDkKcfHWzQ7-A1htN --description "docker" --tag-list docker --executor docker --docker-image "docker:stable" --docker-privileged --run-untagged --locked="false"

docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token 41KQXM6zCNz8i1nyqn6m --description "docker" --tag-list docker --executor docker --docker-image "docker:stable" --docker-volumes /etc/hosts:/etc/hosts --docker-volumes /var/run/docker.sock:/var/run/docker.sock --docker-volumes /etc/gitlab-runner/certs/ca.crt:/etc/gitlab-runner/certs/ca.crt

docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token Y4J9GXLHjJm5xp9cQ7z9 --description "docker" --tag-list docker --executor docker --docker-image "docker:stable" --docker-volumes /etc/hosts:/etc/hosts --docker-volumes /var/run/docker.sock:/var/run/docker.sock --docker-volumes /etc/gitlab-runner/certs/ca.crt:/etc/gitlab-runner/certs/ca.crt

docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token 3kz1WCsgXJB3Wuj1xPRJ --description "shell" --tag-list shell --executor shell
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

/etc/ssl/certs/ca-certificates.crt
