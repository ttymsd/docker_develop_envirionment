FROM ubuntu

MAINTAINER Tetsuya Masuda <ttymsd@gmail.com>

ENV DEBIAN_FRONTEND noninteractive

# Install dependencies
RUN apt-get update && \
  apt-get install -yq apache2 --no-install-recommends && \
  apt-get clean

VOLUME ["/documents/html_mock", "/documents/app_download", "/documents/api_doc"]

RUN ln -s /documents/html_mock /var/www/html/html_mock 
RUN ln -s /documents/app_download /var/www/html/app_download
RUN ln -s /documents/app_api_doc /var/www/html/api_doc

COPY ports.conf /etc/apache2/ports.conf
COPY 000-default.conf /etc/apache2/sites-enabled/000-default.conf

ENTRYPOINT service apache2 start && \
  sleep 5 && \
  tail -f /var/log/apache2/access.log
