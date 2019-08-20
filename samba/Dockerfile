## https://github.com/pwntr/samba-alpine-docker
#FROM stanback/alpine-samba
#FROM pwntr/samba-alpine
#FROM joebiellik/samba-server

FROM alpine

ENV SAMBA_USER=www-data
ENV SAMBA_PASSWORD=www-data
ENV SAMBA_GROUP=www-data
ENV SAMBA_HOME="/var/www"
#ENV WORKGROUP=VEVVA
#ENV HOSTNAME=samba

RUN apk add --no-cache \
        samba-server \
        samba-common-tools \
        supervisor \
## Create a system user without password, no shell and gid/uid 1000!!!
&&  addgroup -g 1000 ${SAMBA_GROUP} \
&&  adduser -u 1000 ${SAMBA_USER} -D -G ${SAMBA_GROUP} -h ${SAMBA_HOME} -s /bin/false \
## Create a samba user
&&  echo -e "${SAMBA_PASSWORD}\n${SAMBA_PASSWORD}" | smbpasswd -s -a ${SAMBA_USER}

## Create shared folder
#RUN mkdir -p ${SAMBA_HOME}/html; \
#    chown -R ${SAMBA_USER}:${SAMBA_GROUP} ${SAMBA_HOME}

## Samba configuration
#RUN cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
COPY config/smb.conf /etc/samba/smb.conf

#VOLUME /var/www/html

## Samba 135 for End Point Mapper [DCE/RPC Locator Service], 137, 138 for nmbd and 139, 445 for smbd
#EXPOSE 135/tcp 137/udp 138/udp 139/tcp 445/tcp
EXPOSE 445/tcp

## Supervisor
COPY config/supervisord.conf /
ENTRYPOINT ["supervisord", "-c", "/supervisord.conf"]



#CMD ["/usr/sbin/smbd", "foreground", "no-process-group"]
#CMD /usr/sbin/smbd -FS -d3 < /dev/null
#CMD /usr/sbin/smbd -FS -d3 < /dev/null
#CMD /usr/sbin/smbd < /dev/null

#ENTRYPOINT ["/entrypoint.sh"]
#CMD ["/usr/sbin/smbd", "-s", "/etc/samba/smb.conf", "-F", "-S"]

#CMD ["/usr/sbin/smbd", "-D"]
#CMD ["/usr/sbin/smbd", "-FS"]
#CMD ["/usr/sbin/smbd", "-FSD"]
#CMD ["/usr/sbin/smbd", "-i", "-F"]
#CMD /sbin/smbd -i -F
#CMD /usr/sbin/smbd -D "$@"
