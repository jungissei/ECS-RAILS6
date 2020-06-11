FROM ruby:2.6.3


RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - \
&& echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list

RUN curl -sL https://deb.nodesource.com/setup_10.x | bash && apt-get update -qq && \
apt-get install -y build-essential libpq-dev nodejs yarn vim


RUN apt-get update -qq && \
  apt-get install -y apt-utils \
  build-essential \
  libpq-dev \
  nodejs \
  yarn \
  vim \
  default-mysql-client 



WORKDIR /app

ADD Gemfile .
ADD Gemfile.lock .
RUN bundle install -j4

ADD . /app


EXPOSE 3000

RUN yarn install --check-files && \
  yarn upgrade && \
  bundle exec rake assets:precompile