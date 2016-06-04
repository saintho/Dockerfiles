FROM andyshinn/dnsmasq:2.75

ADD  dnsmasqhosts      /etc/dnsmasqhosts 
ADD  resolv.dnsmasq    /etc/resolv.dnsmasq
ADD  dnsmasq.conf      /etc/dnsmasq.conf

EXPOSE 53
VOLUME ["/opt"]
