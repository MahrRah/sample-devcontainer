# Dependencies versions
ARG PYTHON_VERSION="3.7.10"

ARG NODE_VERSION="15.x"
ARG MD_SPELLCHECK_VERSION="1.3.1"
ARG MD_LINK_CHECK_VERSION="3.8.6"
ARG MD_LINT_VERSION="0.27.1"

FROM python:${PYTHON_VERSION}-buster

ADD .devcontainer/requirements.txt /tmp/requirements.txt 
RUN  apt-get update \
    # Install Python libraries
    && pip install -r /tmp/requirements.txt  \
    # Install node and npm
    && curl -fsSL https://deb.nodesource.com/setup_${NODE_VERSION} | bash - \
    && apt-get install -y nodejs \
    && apt-get install npm -y \
    # Install Docker CE CLI
    && apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common lsb-release \
    && curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | apt-key add - 2>/dev/null \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get install -y docker-ce-cli \
    # Install the Azure CLI and IoT extension
    && curl -sL https://aka.ms/InstallAzureCLIDeb | bash \
    # Install markdown linters
    && npm install markdown-spellcheck@${MD_SPELLCHECK_VERSION} -g \
    && npm install markdown-link-check@${MD_LINK_CHECK_VERSION} -g \
    && npm install markdownlint-cli@${MD_LINT_VERSION} -g \
    # Install ShellCheck
    && apt-get install shellcheck \
    # Add bash completion
    && apt-get update \
    && apt-get -y install bash-completion \
    && echo "source /usr/share/bash-completion/bash_completion" >> ~/.bashrc \
    # Clean up downloaded files
    && cd ~ \ 
    && rm -rf /tmp/* \
    # Clean up
    && apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*

# Customize bash
RUN \
    # Git command prompt
    git clone https://github.com/magicmonty/bash-git-prompt.git ~/.bash-git-prompt --depth=1 \
    && echo "if [ -f \"$HOME/.bash-git-prompt/gitprompt.sh\" ]; then GIT_PROMPT_ONLY_IN_REPO=1 && source $HOME/.bash-git-prompt/gitprompt.sh; fi" >> "/root/.bashrc" \
    # Add alias
    && echo "alias tf=terraform" >> "/root/.bashrc" 