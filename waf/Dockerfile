FROM ubuntu:24.10

RUN apt update && apt upgrade -y
RUN apt install net-tools iproute2 nano nginx libnginx-mod-stream-geoip2 libnginx-mod-http-geoip2 libnginx-mod-http-modsecurity libnginx-mod-http-headers-more-filter -y

USER root

COPY ./conf/nginx.conf /etc/nginx/
COPY ./conf/modsec/ /etc/nginx/modsec/
COPY ./conf/geoip/ /etc/nginx/geoip/
COPY ./conf/protection.conf /etc/nginx/
COPY ./conf/global_errors.conf /etc/nginx/
COPY ./conf/html/ /var/www/html/

COPY ./conf/options-ssl-nginx.conf /etc/nginx/
COPY ./conf/sites-enabled/ /etc/nginx/sites-enabled/
COPY ./conf/ssl-dhparams.pem /etc/nginx/
COPY ./conf/ssl/ /etc/nginx/ssl/

# Exponer puertos
EXPOSE 80 443

# Health check
HEALTHCHECK --interval=30s --timeout=30s --start-period=5s --retries=3 \
    CMD curl -f http://localhost/ || exit 1

# Comando de inicio
CMD ["nginx", "-g", "daemon off;"]
