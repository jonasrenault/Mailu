# syntax=docker/dockerfile-upstream:1.4.3

# admin image
FROM base

ARG VERSION=local
LABEL version=$VERSION
LABEL org.opencontainers.image.source=https://github.com/jonasrenault/Mailu

RUN set -euxo pipefail \
  ; apk add --no-cache libressl mariadb-connector-c postgresql-libs

COPY --from=assets /work/static/ ./mailu/static/

COPY audit.py /
COPY start.py /

COPY migrations/ ./migrations/

COPY mailu/ ./mailu/
RUN set -euxo pipefail \
  ; venv/bin/pybabel compile -d mailu/translations

RUN echo $VERSION >/version

#EXPOSE 8080/tcp
HEALTHCHECK CMD curl -m3 -skfLo /dev/null http://localhost:8080/ping

VOLUME ["/data","/dkim"]

ENV FLASK_APP=mailu
CMD /start.py
