FROM registry.access.redhat.com/ubi8/openjdk-8
 
USER root
 
ENV NGINX_CONF_PATH=/etc/nginx/nginx.conf \
    NGINX_SSL_DIR=/etc/pki/tls/
 
# Install nginx and crypto policies command
RUN microdnf install -y nginx --nodocs \
    && microdnf install -y crypto-policies-scripts \
    && microdnf clean all
 
# Copy certificates and keys found on ssl dir to default nginx ssl dir
ADD ssl/*.crt ${NGINX_SSL_DIR}/certs/
ADD ssl/*.key ${NGINX_SSL_DIR}/private/
ADD nginx.conf ${NGINX_CONF_PATH}
 
# Add permissions to nginx files to run as normal user
# Create the nginx.pid before the service so it has permissions
RUN chmod a+rwx ${NGINX_CONF_PATH} \
    && chmod -R a+rwx /var/lib/nginx \
    && touch /var/run/nginx.pid \
    && chmod a+rwx /var/run/nginx.pid \
    && chown -R 185:0 /var/run/nginx.pid
 
# Enable legacy protocols on this image
RUN update-crypto-policies --set LEGACY
 
USER 185