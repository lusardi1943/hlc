ARG AUTOR
FROM ${AUTOR}/ubuntubase


ARG USUARIO
ARG CONTEXT
ARG PROYECTO
ARG TZ
ENV USUARIO="pepe"
ENV PASSWORD="abc"

USER root
RUN apt update && apt install -yq --no-install-recommends \
    nginx

# RUN mkdir /root/admin/nginx
COPY ./proyectos/${PROYECTO}/deploy/config/default.conf /etc/nginx/conf.d/default.conf
# verificar en entrypoint la existencia de /etc/nginx/conf.d y /var/www/html
# COPY ./proyectos/${PROYECTO}/deploy/config /root/admin/nginx

# COPY ./proyectos/${PROYECTO}/deploy/html /var/www/html
# RUN mkdir /home/${USUARIO}/app
# COPY ./proyectos/${PROYECTO}/app /home/${USUARIO}/app

RUN chown -R www-data /var/www/html
RUN chmod -R 755 /var/www/html

# instalo nginx/apache --> usuario www-data
# el propietario de /var/www/html debe de ser www-data
RUN mkdir -p /var/log/nginx
EXPOSE 80

USER root
RUN mkdir /root/admin/nginx
COPY ./dockerfiles/sweb/nginx /root/admin/nginx
RUN chmod +x /root/admin/nginx/admin/start.sh

WORKDIR /root/admin/nginx
ENTRYPOINT ["./admin/start.sh"]