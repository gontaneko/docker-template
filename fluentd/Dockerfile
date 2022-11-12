FROM fluent/fluentd:v1.14-1

USER root

RUN apk add --no-cache --update --virtual .build-deps \
        sudo build-base ruby-dev \
 # cutomize following instruction as you wish
 && sudo gem install elasticsearch -v 7.10 \
 && sudo gem install fluent-plugin-elasticsearch \
 && sudo gem install fluent-plugin-forest \
 && sudo gem sources --clear-all \
 && apk del .build-deps \
 && rm -rf /home/fluent/.gem/ruby/2.5.0/cache/*.gem

COPY fluent.conf /fluentd/etc/
COPY entrypoint.sh /bin/
RUN chmod +x /bin/entrypoint.sh

USER fluent
