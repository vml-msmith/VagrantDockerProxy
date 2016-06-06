# Build from Drupal CI web-5.6
FROM drupalci/web-5.5

RUN sudo apt-get install locate

RUN pear channel-discover pear.twig-project.org
RUN pear install twig/CTwig

# Install Node
RUN curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
RUN sudo apt-get install -y nodejs

# Install memcached
RUN sudo apt-get install memcached -y

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php
RUN mv composer.phar /usr/local/bin/composer
RUN echo 'export PATH="$HOME/.composer/vendor/bin:$PATH"' >> ~/.bashrc
RUN export PATH="$HOME/.composer/vendor/bin:$PATH"

# Install Drush dependencies
RUN composer global require consolidation/output-formatters ~1.0.0-beta6
RUN composer global require consolidation/annotated-command ~1.0.0-beta9
RUN composer global require codegyre/robo:~1.0.0-beta1
RUN composer global remove symfony/console

# Install Drush
RUN composer global require drush/drush:8.x

# Install XDebug.ini
COPY xdebug.ini /opt/phpenv/versions/5.5.9/etc/conf.d/xdebug.ini

# php ini settings
RUN echo 'error_reporting=E_ALL' >> /opt/phpenv/versions/5.5.9/etc/php.ini
RUN echo 'display_errors=1' >> /opt/phpenv/versions/5.5.9/etc/php.ini
RUN echo 'display_startup_errors=1' >> /opt/phpenv/versions/5.5.9/etc/php.ini
RUN echo 'log_errors=1' >> /opt/phpenv/versions/5.5.9/etc/php.ini
RUN echo 'html_errors=1' >> /opt/phpenv/versions/5.5.9/etc/php.ini
RUN echo 'extension=gmp.so' >> /opt/phpenv/versions/5.5.9/etc/php.ini
RUN echo 'date.timezone="America/Chicago"' >> /opt/phpenv/versions/5.5.9/etc/php.ini
RUN echo 'include=/opt/phpenv/versions/5.5.9/etc/conf.d/*.ini' >> /opt/phpenv/versions/5.5.9/etc/php.ini


WORKDIR /var/www/

EXPOSE 80 443 22
