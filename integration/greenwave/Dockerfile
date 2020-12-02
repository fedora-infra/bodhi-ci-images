FROM quay.io/factory2/greenwave:prod
LABEL \
  name="greenwave" \
  vendor="Fedora Infrastructure" \
  maintainer="Aurelien Bompard <abompard@fedoraproject.org>" \
  license="MIT"

# fedmsg needs a username.
ENV USER=greenwave

# Become root during build to chmod
USER 0

# Make sure fedmsg can write its CRL.
RUN chmod 777 /var/run/fedmsg/

RUN mkdir -p /etc/greenwave
COPY start.sh /etc/greenwave/start.sh
COPY fedmsg.py /etc/fedmsg.d/zz_greenwave.py
COPY settings.py /etc/greenwave/settings.py
COPY policy.yaml /etc/greenwave/fedora.yaml
COPY fedora-messaging.toml /etc/fedora-messaging/config.toml

# Become non-root again
USER 1001

CMD ["bash", "/etc/greenwave/start.sh"]
