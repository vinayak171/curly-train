# curly-train
 i. Change to root user: 
                $ sudo su
    ii. Install openswan:
                $ yum install openswan -y
    iii. In /etc/ipsec.conf uncomment following line if not already 
          uncommented:
                 include /etc/ipsec.d/*.conf
    iv. Update /etc/sysctl.conf to have following
 net.ipv4.ip_forward = 1
 net.ipv4.conf.all.accept_redirects = 0
 net.ipv4.conf.all.send_redirects = 0
    v. Restart network service:
                 $ service network restart
                 /etc/ipsec.d/aws-vpn.conf
conn Tunnel1
        authby=secret
        auto=start
        left=%defaultroute
        leftid=Customer end Gateway VPN public IP
        right=AWS Virtual private gateway ID- public IP
        type=tunnel
        ikelifetime=8h
        keylife=1h
        phase2alg=aes128-sha1;modp1024
        ike=aes128-sha1;modp1024
        keyingtries=%forever
        keyexchange=ike
        leftsubnet=Customer end VPN CIDR
        rightsubnet=AWS end VPN CIDR
        dpddelay=10
        dpdtimeout=30
        dpdaction=restart_by_peer
