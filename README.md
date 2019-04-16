# Gitlab Sample

## Gen cert, key

```
openssl req -newkey rsa:2048 -x509 -nodes -keyout ./ssl/gitlab.example.com/gitlab.example.com.key -new -out ./ssl/gitlab.example.com/gitlab.example.com.crt -subj /CN=gitlab.example.com -sha256 -days 365
```

## Register Gitlab-Runner

```bash
## Shell Passed
docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token Du6YGsmNCskeZQhPvLDX --description "shell" --tag-list shell --executor shell

## Docker Passed
docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token -jcW4Gy1UPFLsaPaCrxf --description "docker" --tag-list docker --executor docker --docker-image "docker:latest" --docker-network-mode development --docker-volumes /var/run/docker.sock:/var/run/docker.sock --docker-privileged
```

## Options gitlab-ce

```bash
nginx['ssl_protocols'] = "TLSv1 TLSv1.1 TLSv1.2"
nginx['redirect_http_to_https'] = true
nginx['listen_port'] = 443
gitlab_rails['time_zone'] = 'Asia/Bangkok'
registry_nginx['ssl_certificate'] = "/etc/gitlab/ssl/registry.example.com.pem"
registry_nginx['ssl_certificate_key'] = "/etc/gitlab/ssl/registry.example.com.key"
registry_nginx['listen_https'] = false
registry_nginx['listen_port'] = 8888

# ca-certificates.crt path of gitlab-runner
/etc/ssl/certs/ca-certificates.crt
```

## Unavailable name for jobs

> Each job must have a unique name, but there are a few reserved keywords that cannot be used as job names:

- image
- services
- stages
- types
- before_script
- after_script
- variables
- cache
