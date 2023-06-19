FROM debian:11-slim as download

ARG hugo_version="0.112.7"

RUN apt-get update \
    && apt-get install -y wget \
    && hugo_arch="$(dpkg --print-architecture)" \
    && wget https://github.com/gohugoio/hugo/releases/download/v${hugo_version}/hugo_extended_${hugo_version}_linux-${hugo_arch}.tar.gz \
    && tar -xvzf hugo_extended_${hugo_version}_linux-${hugo_arch}.tar.gz

FROM debian:11-slim

ENV DEBIAN_FRONTEND=noninteractive
COPY --from=download hugo /usr/local/bin/hugo
COPY resources/sudoers.d/vscode.conf /etc/sudoers.d/vscode
RUN chmod a+x /usr/local/bin/hugo \
    && apt-get update \
    && apt-get install -y \
    ca-certificates \
    npm \
    golang \
    git \
    sudo

RUN groupadd wheel \
    && useradd -G wheel -ms /bin/bash vscode

CMD ["hugo"]