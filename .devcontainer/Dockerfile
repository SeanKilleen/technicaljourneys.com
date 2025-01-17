# Adapted from https://github.com/timbru31/docker-ruby-node/blob/master/2.7/16/Dockerfile
# Using dependency references from https://pages.github.com/versions/

# 2.7.3 is GitHub Pages 226 compatible
ARG RUBY_VERSION=2.7.3


FROM ruby:${RUBY_VERSION}

ARG GH_PAGES_VERSION=226
ARG NODE_MAJOR_VERSION=16

LABEL maintainer="Sean Killeen <SeanKilleen@gmail.com>"

VOLUME /docs

WORKDIR /docs

######################################################
#             Installling Base + Ruby Stuff          #
######################################################

RUN apt-get -y update

RUN apt-get -y install \
    git \
    tzdata \
    dos2unix

RUN gem install bundler

#################################################################
#                  Installing node                              #
#################################################################

RUN curl -sL https://deb.nodesource.com/setup_${NODE_MAJOR_VERSION}.x | bash -\
  && apt-get update -qq && apt-get install -qq --no-install-recommends \
    nodejs \
  && apt-get upgrade -qq \
  && apt-get clean \
  && rm -rf /var/lib/apt/lists/*\
  && npm install -g yarn@1

RUN node -v
RUN npm -v
RUN npm install -g cspell markdownlint-cli

COPY aliases.sh /etc/profile.d/alias.sh

# Coverts CRLF based files (such as those on windows devices) to LF line endings for container
RUN dos2unix /etc/profile.d/alias.sh

RUN cat /etc/profile.d/alias.sh >> ~/.bashrc

EXPOSE 4000
