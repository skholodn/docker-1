FROM golang
MAINTAINER skholodn@student.unit.ua
RUN apt-get update -y && apt-get upgrade -y && \
	adduser --disabled-login --gecos 'Gogs' git && \
	mkdir -p /go/src/github.com/gogits && \
	cd /go/src/github.com/gogits && \
# Make sure you don't use "https://github.com/gogits/gogs.git"
	git clone --depth=1 -b develop https://github.com/gogits/gogs && \
	cd gogs && \
	go build && \
	apt-get install libpam0g-dev && \
	go get -u -tags "sqlite pam cert" github.com/gogits/gogs && \
	cd /go/src/github.com/gogits/gogs && \
	go build -tags "sqlite pam cert"
WORKDIR /go/src/github.com/gogits/gogs
EXPOSE 3000
CMD ["./gogs", "web"]