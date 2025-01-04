services:
  pihole:
    container_name: piholetest
    image: pihole/pihole:latest
    hostname: piholetest
    networks:
      pihole_network:
        ipv4_address: '10.0.0.51' #update IP
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "67:67/udp"
      - "80:80/tcp"
    environment:
      TZ: 'Europe/London'
      WEBPASSWORD: '*****' #update password
    volumes:
      - '/home/alstonb/pihole/etc-pihole:/etc/pihole' #update location
      - '/home/alstonb/pihole/etc-dnsmasq.d:/etc/dnsmasq.d' #update location
    cap_add:
      - NET_ADMIN
    restart: unless-stopped

networks:
  pihole_network:
    driver: macvlan
    driver_opts:
      parent: eth0 #update ethernet adapter
    ipam:
      config:
        - subnet: 10.0.0.0/8 #update network subnet range
          gateway: 10.0.0.1 #update gateway IP
