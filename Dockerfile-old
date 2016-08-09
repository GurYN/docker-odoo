# ------------------------------------------------------------------ #
# Name        : Odoo 9.0 all-in-one                                  #
# Package     : vcibelli/odoo                                        #
# Version     : 9.0                                                  #
# Description : Odoo 9 image based on Ubuntu 16.04 LTS               #
# ------------------------------------------------------------------ #

# Use of Ubuntu base image
FROM jedisct1/phusion-baseimage-latest:16.04

# Maintainer
MAINTAINER Vincent CIBELLI <v.cibelli@outlook.com>

# Get wget binaries
RUN apt-get update && apt-get -y install wget

# Get Odoo and dependencies binaries
RUN wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
RUN echo "deb http://nightly.odoo.com/9.0/nightly/deb/ ./" >> /etc/apt/sources.list
RUN apt-get update && apt-get -y install odoo

# Add wkhtmltopdf binaries
RUN apt-get remove --purge wkhtmltopdf
RUN wget http://download.gna.org/wkhtmltopdf/0.12/0.12.1/wkhtmltox-0.12.1_linux-trusty-amd64.deb
RUN dpkg -i wkhtmltox-0.12.1_linux-trusty-amd64.deb
RUN cp /usr/local/bin/wkhtmltopdf /usr/bin
RUN cp /usr/local/bin/wkhtmltoimage /usr/bin

# Add custom modules path
RUN mkdir /mnt/extra-addons
ADD openerp-server.conf /etc/odoo/openerp-server.conf

# Add odoo role in postgresql
RUN /etc/init.d/postgresql start &&\
    su postgres -c "psql --command \"CREATE USER odoo WITH SUPERUSER PASSWORD 'odoo';\" "

# Add volumes
VOLUME ["/etc/odoo", "/mnt/extra-addons"]

# Expose 8069 port
EXPOSE 8069

# Add Startup tasks
ENTRYPOINT service postgresql start && service odoo start && /sbin/my_init