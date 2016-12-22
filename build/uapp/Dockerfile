FROM ubuntu:trusty

ENV RUBY_VERSION=2.3.3 \
    DEV_USER=ubuntu

USER root
RUN BASE_PACKAGE="build-essential autoconf bison nodejs libssl-dev libffi-dev libsqlite3-dev libmysqlclient-dev postgresql-client zlib1g-dev libmagickwand-dev libreadline6-dev libncurses5-dev libxml2-dev libxslt-dev libyaml-dev libgdbm-dev" \
    EDIT_PACKAGE="vim tmux wget gawk curl git ca-certificates openssl silversearcher-ag imagemagick" && \
    apt-get update -y && \
    apt-get install -y --no-install-recommends ${BASE_PACKAGE} ${EDIT_PACKAGE} && \
    apt-get autoremove && apt-get autoclean && \
    useradd -m -s /bin/bash ${DEV_USER} && \
    echo "${DEV_USER}        ALL=(ALL)       NOPASSWD: ALL" > /etc/sudoers.d/${DEV_USER}

# rbenv install
USER ${DEV_USER}
WORKDIR /home/${DEV_USER}

RUN RUBY_PACKAGE_VERSION=${RUBY_VERSION} \
    PATH=/home/${DEV_USER}/.rbenv/bin:${PATH} && mkdir -p ~/bin && \
    # ruby environment install
    git clone https://github.com/rbenv/rbenv.git ~/.rbenv && \
    git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build && \
    git clone https://github.com/rbenv/rbenv-gem-rehash.git ~/.rbenv/plugins/rbenv-gem-rehash && \
    echo 'export PATH=${HOME}/.rbenv/bin:${HOME}/bin:${PATH} ; eval "$(rbenv init -)"' >> ~/.bashrc && \
    echo "install: --no-ri --no-rdoc\nupdate: --no-ri --no-rdoc" > ~/.gemrc && \
    rbenv install ${RUBY_PACKAGE_VERSION} && rbenv global ${RUBY_PACKAGE_VERSION} && \
    rbenv exec gem install bundler && \
    # etc tool
    wget -q https://dl.minio.io/client/mc/release/linux-amd64/mc -O ~/bin/mc && chmod +x ~/bin/mc

COPY Gemfile Gemfile.templates
EXPOSE 3000
