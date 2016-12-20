FROM ubuntu:trusty

ENV RUBY_VERSION=2.3 \
    DEV_USER=ubuntu

USER root
RUN BASE_PACKAGE="autoconf bison build-essential nodejs libssl-dev libffi-dev libsqlite3-dev libmysqlclient-dev postgresql-client zlib1g-dev libmagickwand-dev libreadline6-dev libncurses5-dev libxml2-dev libxslt-dev libyaml-dev libgdbm-dev" \
    EDIT_PACKAGE="vim tmux wget curl git ca-certificates silversearcher-ag imagemagick" && \
    #  sliversearcher-ag
    apt-get update -y && \
    apt-get install -y --no-install-recommends ${BASE_PACKAGE} ${EDIT_PACKAGE} && \
    useradd -m -s /bin/bash ${DEV_USER}

# rbenv install
USER ${DEV_USER}
RUN RUBY_PACKAGE_VERSION=${RUBY_VERSION}.3 \
    RUBY_DEVELOP_VERSION=${RUBY_VERSION}.0 && \
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv && \
    git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build && \
    git clone https://github.com/sstephenson/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash && \
    echo 'export PATH=${HOME}/.rbenv/bin:${PATH}' >> ~/.bashrc && \
    echo 'eval "$(rbenv init -)"' >> ~/.bashrc && \
    # ruby environment install
    echo "install: --no-ri --no-rdoc\nupdate: --no-ri --no-rdoc" > ~/.gemrc && \
    PATH=${HOME}/.rbenv/bin:${PATH} && \
    rbenv install ${RUBY_PACKAGE_VERSION} && rbenv global ${RUBY_PACKAGE_VERSION} && \
    rbenv install ${RUBY_DEVELOP_VERSION}-dev && \
    # ruby bundler
    rbenv exec gem install bundler

WORKDIR /home/${DEV_USER}

EXPOSE 3000
