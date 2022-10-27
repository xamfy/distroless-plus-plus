# Java Version: 17
# Debian Version: 11
# Other binaries/tools: curl
# Credits for this approach: Anders F Björklund (minikube maintainer, https://github.com/afbjorklund)

FROM debian:11 AS build-env

RUN apt-get update && apt-get install -y curl && rm -rf /var/lib/apt/lists/*
ADD https://www.cyberciti.biz/files/lighttpd/l2chroot.txt /usr/local/bin/l2chroot
RUN chmod 755 /usr/local/bin/l2chroot
RUN mkdir -p /webroot/usr/bin
RUN /bin/cp /usr/bin/curl /webroot/usr/bin/curl
RUN l2chroot /usr/bin/curl

FROM gcr.io/distroless/java17-debian11
COPY --from=build-env /webroot/usr/ /usr/
COPY --from=build-env /webroot/lib/ /lib/
CMD ["/usr/bin/curl"]
