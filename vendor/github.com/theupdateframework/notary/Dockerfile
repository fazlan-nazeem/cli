FROM golang:1.14.1@sha256:38a520b05b971181a5a30d72b74d1b70c63688eb267a4fb376c7476a5c6f885b

RUN apt-get update && apt-get install -y \
	curl \
	clang \
	libsqlite3-dev \
	patch \
	tar \
	xz-utils \
	python \
	python-pip \
	python-setuptools \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN useradd -ms /bin/bash notary \
	&& pip install codecov \
	&& go get golang.org/x/lint/golint github.com/fzipp/gocyclo github.com/client9/misspell/cmd/misspell github.com/gordonklaus/ineffassign github.com/securego/gosec/cmd/gosec/...

ENV NOTARYDIR /go/src/github.com/theupdateframework/notary

COPY . ${NOTARYDIR}
RUN chmod -R a+rw /go && chmod 0600 ${NOTARYDIR}/fixtures/database/*

ENV GO111MODULE=on

WORKDIR ${NOTARYDIR}
