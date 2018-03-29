FROM ruby
MAINTAINER skholodn@student.unit.ua
ONBUILD COPY . /opt/app
ONBUILD WORKDIR /opt/app 
ONBUILD RUN apt-get update -y && apt-get upgrade -y && \ 
    gem install rails && \
    apt-get install -y nodejs
EXPOSE 3000
ONBUILD RUN bundle update && bundle install && rails db:migrate && rails db:seed