FROM debian

RUN apt update &&\
  apt upgrade -y &&\
  apt install -y --no-install-recommends libapache2-mod-security2 apache2 &&\
  rm -r /var/lib/apt/lists/*
  
RUN a2enmod security2 &&\
  cp /etc/modsecurity/modsecurity.conf-recommended /etc/modsecurity/modsecurity.conf &&\
  sed -i 's/^SecAuditLogParts .*/SecAuditLogParts B/g' /etc/modsecurity/modsecurity.conf &&\
  sed -i 's|^SecAuditLog .*|SecAuditLog /proc/self/fd/1|g' /etc/modsecurity/modsecurity.conf &&\
  sed -i 's/^SecAuditEngine .*/SecAuditEngine On/g' /etc/modsecurity/modsecurity.conf &&\
  sed -i 's/^SecRuleEngine .*/SecRuleEngine On/g' /etc/modsecurity/modsecurity.conf

COPY modsecurity-host.conf /etc/modsecurity/
COPY start.sh /start.sh

EXPOSE 80
ENTRYPOINT ["/start.sh"]
