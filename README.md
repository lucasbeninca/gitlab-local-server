# docker-gitlab-local-install
getting startd docker in local server

-----------------------------------------------------------------------------------------
LOCAR COM ROOT 
usuário root
DEFINIR
senha gitlab local 
EXAMPLE: 12345678

-----------------------------------------------------------------------------------------

accestoken cypress intermediário
CRIE UM ACESSTOKEN

-----------------------------------------------------------------------------------------

accestoken ci-pipelines
CRIE UM ACESSTOKEN

-----------------------------------------------------------------------------------------

CRIAR CHAVE SSH 



-----------------------------------------------------------------------------------------
docker run
docker pull wlsf82/gitlab-ce

docker run --publish 80:80 --publish 22:22 --hostname localhost wlsf82/gitlab-ce

-----------------------------------------------------------------------------------------
Crie o diretório:

sudo mkdir -p /srv/gitlab

Se você estiver executando o Docker com um usuário diferente de root, conceda as permissões apropriadas ao usuário para o novo diretório.

Configure uma nova variável de ambiente $GITLAB_HOMEque defina o caminho para o diretório que você criou:

export GITLAB_HOME=/srv/gitlab




sudo docker run --detach \
   --hostname localhost \
   --env GITLAB_OMNIBUS_CONFIG="external_url 'http://gitlab.example.com'" \
   --publish 443:443 --publish 80:80 --publish 22:22 \
   --name gitlab \
   --restart always \
   --volume $GITLAB_HOME/config:/etc/gitlab \
   --volume $GITLAB_HOME/logs:/var/log/gitlab \
   --volume $GITLAB_HOME/data:/var/opt/gitlab \
   --shm-size 256m \
   gitlab/gitlab-ce:latest


-----------------------------------------------------------------------------------------


adicionando runner

docker pull gitlab/gitlab-runner:latest

docker run -d --name gitlab-runner \
  --restart always \
  --volume /srv/gitlab-runner/config:/etc/gitlab-runner \
  --volume /var/run/docker.sock:/var/run/docker.sock \
  gitlab/gitlab-runner:latest
-----------------------------------------------------------------------------------------

