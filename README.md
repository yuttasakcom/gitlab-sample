# Gitlab Sample

## Register Gitlab-Runner

```bash
docker-compose exec gitlab-runner gitlab-runner register -n --tls-ca-file /ssl/gitlab.example.com/gitlab.example.com.crt --tls-key-file /ssl/gitlab.example.com/gitlab.example.com.key --url https://gitlab.example.com --registration-token m6TsAsyYWQf_bCftrzbZ --description "docker-runner" --tag-list build --executor docker --docker-image "docker:latest" --docker-privileged
```

gitlab-runner register -n \
 --url https://gitlab.example.com/ \
 --registration-token m6TsAsyYWQf_bCftrzbZ \
 --executor docker \
 --description "docker-builder" \
 --docker-image "docker:latest" \
 --docker-privileged

cat /etc/gitlab/ssl/gitlab.example.com.
gitlab.example.com.crt gitlab.example.com.key

docker cp 330d560ac395:/etc/gitlab/ssl/gitlab.example.com.crt .
docker cp 330d560ac395:/etc/gitlab/ssl/gitlab.example.com.key .

nginx['ssl_protocols'] = "TLSv1 TLSv1.1 TLSv1.2"
nginx['redirect_http_to_https'] = true
nginx['listen_port'] = 443
gitlab_rails['time_zone'] = 'Asia/Bangkok'
