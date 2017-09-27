FROM zambon/agent-base:v0.3.0

ARG ARCH

ENV CNI v0.3.0
ENV RANCHER_CNI_IPAM v0.1.1
ENV RANCHER_CNI_BRIDGE v0.5.0

ENV CNI_URL=https://github.com/zambon/rancher__cni/releases/download/${CNI}/cni-${CNI}-${ARCH}.tgz \
    CNI_IPAM_URL=https://github.com/zambon/rancher__rancher-cni-ipam/releases/download/${RANCHER_CNI_IPAM}/rancher-cni-ipam-${RANCHER_CNI_IPAM}-${ARCH}.tar.gz \
    CNI_BRIDGE_URL=https://github.com/zambon/rancher__rancher-cni-bridge/releases/download/${RANCHER_CNI_BRIDGE}/rancher-cni-bridge-${RANCHER_CNI_BRIDGE}-${ARCH}.tar.gz

ADD strongswan.tar.gz /
RUN mkdir -p /opt/cni/bin /etc/cni/net.d /usr/local/etc/strongswan.d \
    && curl -sfSL ${CNI_URL} | tar xvzf - -C /tmp ./loopback \
    && curl -sfSL ${CNI_IPAM_URL} | tar xvzf - -C /tmp \
    && curl -sfSL ${CNI_BRIDGE_URL} | tar xvzf - -C /tmp \
    && mv /tmp/rancher-cni-bridge /tmp/rancher-bridge \
    && mv /tmp/* /opt/cni/bin

COPY charon.conf /usr/local/etc/strongswan.d/charon.conf
COPY start.sh start-vxlan.sh rancher-net /usr/bin/
CMD ["start.sh"]
