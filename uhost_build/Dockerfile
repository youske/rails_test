FROM ubuntu:trusty

ENV RUBY_VERSION=2.3.1 \
    DEV_USER=ubuntu

USER root
RUN BASE_PACKAGE="autoconf bison build-essential nodejs libssl-dev libffi-dev libsqlite3-dev zlib1g-dev libreadline6-dev libncurses5-dev libxml2-dev libxslt-dev libyaml-dev libgdbm-dev" \
    EDIT_PACKAGE="vim tmux wget curl git ca-certificates silversearcher-ag" && \
    #  sliversearcher-ag
    apt-get update && \
    apt-get install -y --no-install-recommends ${BASE_PACKAGE} ${EDIT_PACKAGE} && \
    useradd -m -s /bin/bash ${DEV_USER}

# rbenv install
USER ${DEV_USER}
COPY Gemfile ~/Gemfile
RUN git clone https://github.com/rbenv/rbenv.git ~/.rbenv && \
    git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build && \
    echo 'export PATH=${HOME}/.rbenv/bin:${PATH}' >> ~/.bashrc && \
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc && \
    # ruby environment install
    echo "install: --no-ri --no-rdoc\nupdate: --no-ri --no-rdoc" > ~/.gemrc && \
    PATH=${HOME}/.rbenv/bin:${PATH} && \
    rbenv install ${RUBY_VERSION} && rbenv global ${RUBY_VERSION} && \
    # ruby bundler
    rbenv exec gem install bundler

EXPOSE 3000
