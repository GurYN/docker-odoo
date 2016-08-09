# docker-odoo

A DockerFile to produce an odoo container all-in-one. This container include all dependencies to use Odoo in a standalone mode.
An official Odoo container exist, you can find it at [https://hub.docker.com/_/odoo/]

Thanks to 'jedisct1' for the excellent base image of Ubuntu, you can find it at [https://hub.docker.com/r/jedisct1/phusion-baseimage-latest/]

## Docker image creation

You can create the image with the following command :
'''
$ docker build -t vcibelli/odoo .
'''

## Start an Odoo instance
This example start an Odoo 9 instance as a daemon with name 'odoo' and redirect 8069 port to local machine:
'''
$ docker run -d -p 8069:8069 --name odoo vcibelli/odoo
'''

## Start an Odoo instance with custom configuration
'''
$ docker run -d -p 8069:8069 -v /your/path/to/custom/configuration:/etc/odoo --name odoo vcibelli/odoo
'''

## Start an Odoo instance with custom addons path
'''
$ docker run -d -p 8069:8069 -v /your/path/to/custom/addons:/mnt/extra-addons --name odoo vcibelli/odoo
'''

## Start or Stop an Odoo instance
'''
$ docker start odoo
$ docker stop odoo
'''