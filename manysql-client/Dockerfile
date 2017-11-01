FROM alpine:latest

RUN apk update --no-cache && \
	apk add --update \
		python \
		python-dev \
		py-pip \
		build-base \
		ca-certificates \
		mariadb-client \
		postgresql-client \
		sqlite \
		bash \
		wget

RUN update-ca-certificates

RUN rm -rf /var/cache/apk/*
		
RUN wget -O /usr/local/bin/dumb-init https://github.com/Yelp/dumb-init/releases/download/v1.2.0/dumb-init_1.2.0_amd64
RUN chmod +x /usr/local/bin/dumb-init
RUN ln -s /usr/bin/sqlite3 /usr/bin/sqlite
RUN pip install virtualenv alembic

WORKDIR /opt/app

COPY requirements.txt .
ONBUILD RUN virtualenv /opt/env && /env/bin/pip install -r /opt/app/requirements.txt

ENTRYPOINT ["/usr/local/bin/dumb-init", "--"]
