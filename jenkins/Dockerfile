FROM jenkins/jenkins:lts

USER root

# Update & Install package #
RUN apt update
RUN apt install fontconfig awscli wget docker.io jq -y
RUN curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
RUN curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
RUN mv kubectl /usr/local/bin/kubectl
RUN chmod +x /usr/local/bin/docker-compose
RUN chmod +x /usr/local/bin/kubectl
RUN usermod -u 1001 jenkins && groupmod -g 1001 jenkins
RUN groupmod -g 988 docker || groupadd -g 988 docker
RUN usermod -aG docker jenkins
RUN wget https://releases.hashicorp.com/terraform/1.5.7/terraform_1.5.7_linux_amd64.zip \
    && unzip terraform_1.5.7_linux_amd64.zip -d /usr/local/bin \
    && rm terraform_1.5.7_linux_amd64.zip


# Switch back to jenkins user
USER jenkins