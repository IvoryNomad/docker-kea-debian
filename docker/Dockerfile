# syntax=docker/dockerfile:1
FROM nnorman9/docker-supervisord-debian:bookworm

RUN <<EOT /bin/bash
    apt-get update
    apt-get upgrade -y
    apt-get install --no-install-recommends -y \
        kea-ctrl-agent \
        kea-dhcp-ddns-server \
        kea-dhcp4-server \
        kea-admin
    apt-get remove -y make gcc git wget gettext
    apt-get autoremove -y
    apt-get clean
    rm -rf /var/lib/apt/lists/*
    rm -rf /var/cache/* /var/log/* /tmp/* /var/lib/dpkg/status-old
EOT

RUN mkdir -p /opt/kea/leases /var/run/kea
COPY ./files/config /etc/kea
COPY ./files/kea-supervisor.conf /etc/supervisor/conf.d
VOLUME [ "/etc/kea", "/var/log/kea", "/opt/kea/leases" ]
EXPOSE 8086
