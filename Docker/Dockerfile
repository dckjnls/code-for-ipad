# TODO: Add docker, docker-compose, omf, nvim config, jdk, node.js, python
### STAGE 1: Create the base image with the newest updates ###
FROM codercom/code-server:latest as base
RUN sudo apt update && sudo apt upgrade -y
RUN sudo apt install -y git wget curl neovim fish
RUN mkdir /home/coder/.jdks
RUN wget \
      -O - https://github.com/AdoptOpenJDK/semeru11-binaries/releases/download/jdk-11.0.12%2B7_openj9-0.27.0/ibm-semeru-open-jdk_x64_linux_11.0.12_7_openj9-0.27.0.tar.gz | \
      tar -xvzf - -C /home/coder/.jdks

# TODO: YAML
### STAGE 2: add extensions to vscode ###
FROM base as extensions
# RUN code-server --install-extension mads-hartmann.bash-ide-vscode
# General
RUN code-server --install-extension gruntfuggly.todo-tree --force
RUN code-server --install-extension zhuangtongfa.material-theme --force
RUN code-server --install-extension vscodevim.vim --force
RUN code-server --install-extension ms-azuretools.vscode-docker --force
RUN code-server --install-extension EditorConfig.EditorConfig --force
RUN code-server --install-extension eamodio.gitlens --force
RUN code-server --install-extension donjayamanne.githistory --force
# RUN code-server --install-extension ms-vscode-remote.remote-ssh --force
# Java
RUN code-server --install-extension vscjava.vscode-java-pack --force
RUN code-server --install-extension GabrielBB.vscode-lombok --force
# Python
RUN code-server --install-extension ms-python.python --force
# RUN code-server --install-extension ms-python.vscode-pylance --force
# JavaScript / TypeScript / Frameworks
RUN code-server --install-extension dsznajder.es7-react-js-snippets --force
RUN code-server --install-extension formulahendry.auto-complete-tag --force
# RUN code-server --install-extension steoates.autoimport --force
RUN code-server --install-extension dbaeumer.vscode-eslint --force
RUN code-server --install-extension redhat.vscode-yaml --force
RUN code-server --install-extension stevencl.adddoccomments --force
# Markdown
RUN code-server --install-extension yzhang.markdown-all-in-one --force
RUN code-server --install-extension shd101wyy.markdown-preview-enhanced --force

### STAGE 3: additional configs ###
FROM extensions as final
RUN sudo chsh -s /usr/bin/fish coder
RUN git config --global user.email "dack.janiels@gmail.com"
RUN git config --global user.name "Dack Janiels"