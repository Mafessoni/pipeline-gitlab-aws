# pipeline-gitlab-aws

```PARA INSTALAR O RUNNER NO SEU GITLAB```

https://docs.gitlab.com/runner/install/linux-manually.html
Using binary file

bash sudo chmod +x /usr/local/bin/gitlab-runner

sudo useradd --comment 'GitLab Runner' --create-home gitlab-runner --shell /bin/bash

sudo gitlab-runner install --user=gitlab-runner --working-directory=/home/gitlab-runner

sudo gitlab-runner start

Para adicionar o runner ao seu projeto:
sudo gitlab-runner register
Utilize a URL do seu gitlab e o token gerado por ele

Depois desse passo execute o comando:
gitlab-runner verify

Caso precise execute novamente:
sudo gitlab-runner start


```CONFIGURAÇÕES DO GIT-RUNNER```
nano /etc/gitlab-runner/config.toml

{
concurrent = 1
check_interval = 0
shutdown_timeout = 0

[session_server]
  session_timeout = 1800

[[runners]]
  name = "conxpert-server"
  url = "http://seugitlab.com/"
  id = 51
  token = "TOKEN_RUNNER"
  token_obtained_at = 2023-10-26T22:20:47Z
  token_expires_at = 0001-01-01T00:00:00Z
  executor = "docker"
  [runners.docker]
	tls_verify = false
	image = "docker:latest"
	privileged = true
	disable_cache = false
	volumes = ["/var/run/docker.sock:/var/run/docker.sock", "/cache"]
	shm_size = 0
	extra_hosts = [""]

  [runners.cache]
	MaxUploadedArchiveSize = 0
}
