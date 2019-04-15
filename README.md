# Gitlab Sample

## Gen cert, key

```
openssl req -newkey rsa:2048 -x509 -nodes -keyout ./ssl/gitlab.example.com/gitlab.example.com.key -new -out ./ssl/gitlab.example.com/gitlab.example.com.crt -subj /CN=gitlab.example.com -sha256 -days 365
```

## Register Gitlab-Runner

```bash
## Shell Passed
docker-compose exec gitlab-runner gitlab-runner register -n -tls-ca-file /etc/gitlab-runner/certs/ca.crt --url https://gitlab.example.com --registration-token 3kz1WCsgXJB3Wuj1xPRJ --description "shell" --tag-list shell --executor shell
```

## Options gitlab-ce

```bash
nginx['ssl_protocols'] = "TLSv1 TLSv1.1 TLSv1.2"
nginx['redirect_http_to_https'] = true
nginx['listen_port'] = 443
gitlab_rails['time_zone'] = 'Asia/Bangkok'

# ca-certificates.crt path of gitlab-runner
/etc/ssl/certs/ca-certificates.crt
```
