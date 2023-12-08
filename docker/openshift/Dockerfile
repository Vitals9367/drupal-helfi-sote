ARG DRUPAL_DOCKER_TAG=8.2
FROM ghcr.io/vitals9367/drupal-docker-base:8.2-dev

COPY / /var/www/html/
WORKDIR /var/www/html
RUN composer install --no-progress --profile --prefer-dist --no-interaction --no-dev --optimize-autoloader

# Copy ALL deploy scripts
COPY docker/openshift/entrypoints/ /entrypoints
RUN chmod +x /entrypoints/*

COPY docker/openshift/init.sh /

# Copy cron scripts
RUN mkdir /crons
COPY docker/openshift/crons/ /crons
RUN chmod +x /crons/*

# Copy nginx overrides.
COPY docker/openshift/custom.locations /etc/nginx/conf.d/custom.locations
