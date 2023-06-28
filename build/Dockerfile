FROM ubuntu

RUN apt-get update

RUN apt-get install -y \
	curl \
	git \
	sudo \
	vim \
	wget \
	unzip \
	jq \
	apt-transport-https \
	software-properties-common

RUN wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
RUN echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/hashicorp.list

RUN wget -q "https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb"
RUN dpkg -i packages-microsoft-prod.deb
RUN rm packages-microsoft-prod.deb

RUN apt-get update && apt-get install -y powershell terraform

RUN curl -sL https://aka.ms/InstallAzureCLIDeb | bash

RUN curl -s https://raw.githubusercontent.com/terraform-linters/tflint/master/install_linux.sh | bash

RUN curl -sSLo ./terraform-docs.tar.gz https://terraform-docs.io/dl/v0.16.0/terraform-docs-v0.16.0-$(uname)-amd64.tar.gz
RUN tar -xzf terraform-docs.tar.gz && chmod +x terraform-docs && mv terraform-docs /usr/local/bin/terraform-docs

RUN rm -rf /var/lib/apt/lists/*

COPY bin/* /usr/local/bin/.
RUN cd /usr/local/bin && tar -xvf pytree.tgz && rm pytree.tgz
RUN chmod +x /usr/local/bin/tfcheck /usr/local/bin/tf-unused /usr/local/bin/pytree

ARG USER=coder
RUN useradd --groups sudo --no-create-home --shell /bin/bash ${USER} \
	&& echo "${USER} ALL=(ALL) NOPASSWD:ALL" >/etc/sudoers.d/${USER} \
	&& chmod 0440 /etc/sudoers.d/${USER}
USER ${USER}
WORKDIR /home/${USER}