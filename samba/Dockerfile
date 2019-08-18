## https://github.com/pwntr/samba-alpine-docker
#FROM stanback/alpine-samba
#FROM pwntr/samba-alpine
#FROM joebiellik/samba-server

FROM alpine

ENV SAMBA_USER=www-data
ENV SAMBA_PASSWD=www-data
#ENV WORKGROUP=VEVVA
#ENV HOSTNAME=samba

## Upgrade base system and install samba and supervisord
RUN apk --no-cache upgrade; \
    apk --no-cache add \
        samba \
        #samba-common-tools \
        samba-common \
        supervisor

## Samba configuration
#RUN cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
COPY config/smb.conf /etc/samba/smb.conf

## Create shared folder
RUN mkdir -p /var/www/html

# Create system user and set home folder
RUN adduser -S ${SAMBA_USER} -h /var/www; \
    echo -e "${SAMBA_PASSWD}\n${SAMBA_PASSWD}" | smbpasswd -s -a ${SAMBA_USER} 1>/dev/null

# Volume mapping
#VOLUME /var/www/html

## Samba 135 for End Point Mapper [DCE/RPC Locator Service], 137, 138 for nmbd and 139, 445 for smbd
#EXPOSE 135/tcp 137/udp 138/udp 139/tcp 445/tcp
EXPOSE 445/tcp

RUN mkdir /config
COPY config/supervisord.conf /config/
ENTRYPOINT ["supervisord", "-c", "/config/supervisord.conf"]
