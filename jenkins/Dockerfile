ARG JENKINS_VERSION=2.288
FROM jenkins/jenkins:${JENKINS_VERSION}
ARG APT_PROXY=
ARG DIVE_VERSION=0.10.0
ARG DOCKER_CHANNEL=stable
ARG DOCKER_COMPOSE_VERSION=1.29.0
ARG DOCKER_GID=997
ARG GOSS_VERSION=0.3.9
ARG YQ_VERSION=2.4.1

ENV \
  CASC_JENKINS_CONFIG=/var/jenkins_home/casc.yaml \
  JAVA_OPTS=-Djenkins.install.runSetupWizard=false \
  JENKINS_ADMIN_ID=admin \
  JENKINS_ADMIN_PASSWORD=admin \
  JENKINS_URL=http://server_ip:8080/

COPY root/ /

USER root

RUN set -ex; \
  chown -R jenkins: "${JENKINS_HOME}"; \
  ls -la "${JENKINS_HOME}"


USER jenkins

RUN set -eux; \
  /usr/local/bin/install-plugins.sh < /usr/share/jenkins/plugins.txt

USER root

RUN set -eux;\
  # Enable APT_PROXY
 	if [ -n "${APT_PROXY}" ];then \
    echo "Acquire::http { Proxy \"${APT_PROXY}\"; };" > /etc/apt/apt.conf.d/01proxy; \
  fi; \
  # see note below about "*.pyc" files
  export PYTHONDONTWRITEBYTECODE=1; \
  groupadd -fo -g ${DOCKER_GID} docker; \
  DEBIAN_FRONTEND=noninteractive apt-get update; \
  DEBIAN_FRONTEND=noninteractive apt-get -yqq install --no-install-recommends -o Dpkg::Options::="--force-confnew" \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg2 \
    make \
    software-properties-common \
    ; \
  curl -sSfsSL https://download.docker.com/linux/debian/gpg | apt-key add - ; \
  add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/debian $(lsb_release -cs) ${DOCKER_CHANNEL}" ; \
  apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93C4A3FD7BB9C367 ; \
  add-apt-repository "deb http://ppa.launchpad.net/ansible/ansible/ubuntu trusty main"; \
  DEBIAN_FRONTEND=noninteractive  apt-get update ; \
  DEBIAN_FRONTEND=noninteractive  apt-get -yqq --no-install-recommends install \
    ansible \
    docker-ce \
    jq \
    moreutils \
    python-pip \
    python3-pip\
    ; \
  DEBIAN_FRONTEND=noninteractive apt-get clean; \
  rm -rf /var/lib/apt/lists/*; \
  usermod -a -G docker jenkins; \
  curl -sSf -o /usr/local/bin/docker-compose -L https://github.com/docker/compose/releases/download/${DOCKER_COMPOSE_VERSION}/docker-compose-Linux-x86_64; \
  chmod +x /usr/local/bin/docker-compose; \
  curl -sSf -o /usr/local/bin/yq -L https://github.com/mikefarah/yq/releases/download/${YQ_VERSION}/yq_linux_amd64; \
  chmod +x /usr/local/bin/yq; \
  pip3 install --no-cache-dir --upgrade pip; \
  pip3 install --no-cache-dir \
    docker \
    ; \
  pip install --no-cache-dir \
    junit_xml \
  ; \
  sed -i \
    -e "s|^#host_key_checking = .*$|host_key_checking = False|g" \
    -e "s|^#display_skipped_hosts = .*$|display_skipped_hosts = False|g" \
    -e "s|^#strategy = .*$|strategy = free|g" \
    -e "s|^#retry_files_enabled = .*$|retry_files_enabled = False|g" \
    -e "s|^#pipelining = .*$|pipelining = True|g" \
    -e "s|^#accelerate_port = .*$|accelerate_port = 6099|g" \
    -e "s|^#accelerate_timeout = .*$|accelerate_timeout = 30|g"  \
    -e "s|^#accelerate_daemon_timeout = .*$|accelerate_daemon_timeout = 30|g" \
    -e "s|^#callback_whitelist = .*|callback_whitelist = junit|g" \
    /etc/ansible/ansible.cfg; \
  curl -sSL "https://github.com/aelsabbahy/goss/releases/download/v${GOSS_VERSION}/goss-linux-amd64" \
    -o /usr/local/bin/goss; \
  chmod +x /usr/local/bin/goss; \
  curl -sSL "https://github.com/wagoodman/dive/releases/download/v${DIVE_VERSION}/dive_${DIVE_VERSION}_linux_amd64.deb" \
    -o "/tmp/dive_${DIVE_VERSION}_linux_amd64.deb"; \
  dpkg -i "/tmp/dive_${DIVE_VERSION}_linux_amd64.deb"; \
  rm -f "/tmp/dive_${DIVE_VERSION}_linux_amd64.deb"; \
  # some of the steps above generate a lot of "*.pyc" files (and setting "PYTHONDONTWRITEBYTECODE" beforehand doesn't propagate properly for some reason), so we clean them up manually (as long as they aren't owned by a package)
	# find /usr -name '*.pyc' -type f -exec bash -c 'for pyc; do dpkg -S "$pyc" &> /dev/null || rm -vf "$pyc"; done' -- '{}' +; \
  # disable APT_PROXY if it has been specified
 	if [ -n "${APT_PROXY}" ];then \
    rm /etc/apt/apt.conf.d/01proxy; \
  fi

RUN set -ex; \
    chown root:root /usr/local/bin/dgoss; \
    chmod +x /usr/local/bin/dgoss; \
    chmod +x /usr/local/bin/dgoss-ci

USER jenkins
