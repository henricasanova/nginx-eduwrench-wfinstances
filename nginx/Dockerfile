FROM ubuntu:latest

MAINTAINER Henri Casanova <henric@hawaii.edu>

# update repositories
RUN apt update

# set timezone to Hawaii
RUN echo "Pacific/Honolulu" > /etc/timezone && export DEBIAN_FRONTEND=noninteractive && apt-get install -y tzdata

# install nginx
RUN apt -y install nginx

# install basic things
RUN apt -y install vim
RUN apt -y install wget
RUN apt -y install inetutils-ping
RUN apt -y install curl

# Get arguments
ARG NGINX_PORT

ARG NGINX_SERVER_HOSTNAME_EDUWRENCH
ARG EDUWRENCH_FRONTEND_PORT
ARG EDUWRENCH_BACKEND_PORT

ARG NGINX_SERVER_HOSTNAME_WFINSTANCES
ARG WFINSTANCES_UI_PORT
ARG WFINSTANCES_API_PORT

# Create nginx config files
COPY custom-nginx.conf /etc/nginx/custom-nginx.conf

RUN sed -i "s/NGINX_SERVER_HOSTNAME_EDUWRENCH/${NGINX_SERVER_HOSTNAME_EDUWRENCH}/g" /etc/nginx/custom-nginx.conf
RUN sed -i "s/EDUWRENCH_FRONTEND_PORT/${EDUWRENCH_FRONTEND_PORT}/g" /etc/nginx/custom-nginx.conf
RUN sed -i "s/EDUWRENCH_BACKEND_PORT/${EDUWRENCH_BACKEND_PORT}/g" /etc/nginx/custom-nginx.conf

RUN sed -i "s/NGINX_SERVER_HOSTNAME_WFINSTANCES/${NGINX_SERVER_HOSTNAME_WFINSTANCES}/g" /etc/nginx/custom-nginx.conf
RUN sed -i "s/WFINSTANCES_UI_PORT/${WFINSTANCES_UI_PORT}/g" /etc/nginx/custom-nginx.conf
RUN sed -i "s/WFINSTANCES_API_PORT/${WFINSTANCES_API_PORT}/g" /etc/nginx/custom-nginx.conf

# Start nginx 
EXPOSE $NGINX_PORT
STOPSIGNAL SIGQUIT
#CMD ["sleep", "10000"]
CMD ["nginx", "-c", "/etc/nginx/custom-nginx.conf", "-g", "daemon off;"]



