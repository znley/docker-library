
FROM lcr.loongnix.cn/library/debian:sid AS build

RUN apt update && apt install ca-certificates wget -y

RUN wget https://github.com/Loongson-Cloud-Community/mc/releases/download/RELEASE.2024-06-10T16-44-15Z/mc-abi2.0.RELEASE.2024-06-10T16-44-15Z  -O /usr/bin/mc && chmod +x /usr/bin/mc

FROM lcr.loongnix.cn/library/debian:sid

# On Debian the certificate bundle is located at:
# - /etc/ssl/certs/ca-certificates.crt
COPY --from=build /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/

COPY CREDITS /licenses/CREDITS
COPY LICENSE /licenses/LICENSE

COPY --from=build /usr/bin/mc /usr/bin/

RUN mc --version


ENTRYPOINT ["mc"]


