## https://github.com/pwntr/samba-alpine-docker
#FROM stanback/alpine-samba
#FROM pwntr/samba-alpine
#FROM joebiellik/samba-server

FROM alpine

ENV USER_NAME=www-data
ENV USER_PASSWORD=www-data
ENV USER_GROUP=www-data
ENV USER_HOME=/var/www

RUN apk add --no-cache \
        samba-server \
        samba-common-tools \
        supervisor \
## Create user without password, no shell (82 is the standard uid/gid for "www-data" in Alpine)
&&  addgroup -g 82 ${USER_GROUP} \
&&  adduser -u 82 ${USER_NAME} -D -G ${USER_GROUP} -h ${USER_HOME} -s /bin/false \
## Create a samba user
&&  echo -e "${USER_PASSWORD}\n${USER_PASSWORD}" | smbpasswd -s -a ${USER_NAME}

## Samba configuration
#RUN cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
COPY config/smb.conf /etc/samba/smb.conf

## Create shared folder
#RUN mkdir -p ${USER_HOME}/html; \
#    chown -R ${USER_NAME}:${USER_GROUP} ${USER_HOME}

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
