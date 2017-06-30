# From: http://piotrnowicki.com/java/2017/01/09/keycloak-docker-with-ssl-proxy/
# JBoss Keycloak is available as a Docker image. It’s all fun and games until you’ll try to run it behind SSL reverse proxy like I do for all my services. Despite settings all required HTTP headers on the proxy side (Nginx in my case) like:

# proxy_set_header Host $host;
# proxy_set_header X-Real-IP $remote_addr;
# proxy_set_header X-Forwarded-Proto $scheme;
# proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

# it fails to pass all the requests to the Docker Keycloak image (running on Wildfly server). It’s because the Keycloak configuration is not prepared to be run behind the SSL  reverse proxy. Configuring it is quite simple as all you need is to set:

# proxy-address-forwarding="true"
# in the http-listener element in standalone.xml configuration.

# This Dockerfile makes the trick

FROM jboss/keycloak:3.1.0.Final

USER root
RUN yum install -y xmlstarlet

USER jboss
RUN xmlstarlet ed --inplace \
    -N x="urn:jboss:domain:undertow:3.0" \
    -a "//x:http-listener" \
    -t attr \
    -n 'proxy-address-forwarding' \
    -v 'true' \
    /opt/jboss/keycloak/standalone/configuration/standalone.xml

COPY themes/ /opt/jboss/keycloak/themes/


