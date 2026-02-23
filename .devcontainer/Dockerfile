FROM php

RUN apt update \
  && apt install -y \
    curl \
    vim \
    sudo

COPY --from=composer /usr/bin/composer /usr/bin/composer
COPY --from=ghcr.io/mlocati/php-extension-installer /usr/bin/install-php-extensions /usr/bin/

RUN install-php-extensions ctype iconv pcre session simplexml tokenizer mbstring

ARG SUMMARIZER_DEV

RUN groupadd -g 1000 ${SUMMARIZER_DEV} \
  && useradd -g 1000 -u 1000 -ms /bin/bash ${SUMMARIZER_DEV} \
  && echo "${SUMMARIZER_DEV} ALL=(root) NOPASSWD:ALL" > /etc/sudoers.d/${SUMMARIZER_DEV} \
  && chmod 0440 /etc/sudoers.d/${SUMMARIZER_DEV} \
  && mkdir -p  /app \
  && chown -R 1000:1000 /app

USER ${SUMMARIZER_DEV}

WORKDIR /app