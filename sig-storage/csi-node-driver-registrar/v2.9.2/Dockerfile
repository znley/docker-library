FROM lcr.loongnix.cn/library/debian:sid as downloader
RUN apt update -y && apt install wget -y
RUN wget -q -O /csi-node-driver-registrar https://github.com/Loongson-Cloud-Community/node-driver-registrar/releases/download/v2.9.2/csi-node-driver-registrar-v2.9.2-abi2.0
# 冒烟
RUN chmod +x /csi-node-driver-registrar && /csi-node-driver-registrar -version


FROM lcr.loongnix.cn/distroless/static-debian10:latest
LABEL maintainers="Kubernetes Authors"
LABEL description="CSI External Attacher"
COPY --from=downloader /csi-node-driver-registrar /csi-node-driver-registrar
ENTRYPOINT ["/csi-node-driver-registrar"]
