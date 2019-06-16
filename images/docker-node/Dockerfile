FROM ubuntu:16.04

# Replace shell with bash so we can source files
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

ENV NVM_DIR /usr/local/nvm
RUN mkdir -p ${NVM_DIR}
ENV NODE_VERSION 10.15.3
ENV TERM=xterm

RUN apt-get update \
    && DEBIAN_FRONTEND=noninteractive apt-get install -yq wget \
    && wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.34.0/install.sh | bash

RUN chmod a+x $NVM_DIR/nvm.sh

RUN bash -c 'source $NVM_DIR/nvm.sh \
    && source /root/.bashrc \
    && nvm install v$NODE_VERSION \
    && nvm use v$NODE_VERSION'

ENV NODE_PATH $NVM_DIR/versions/node/v$NODE_VERSION/lib/node_modules
ENV PATH $NVM_DIR/versions/node/v$NODE_VERSION/bin:$PATH

RUN DEBIAN_FRONTEND=noninteractive apt-get install -yq vim

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y git-core

WORKDIR /app

ADD package.json /app/

RUN npm install -g yarn
RUN npm install

EXPOSE 4000

#CMD ["yarn", "start"]
CMD ["bash"]
