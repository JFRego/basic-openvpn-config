#Site-to-site server side config (server_ss.conf)


- place ca.crt, chained.crt, ivpn.key and ta.key files in /etc/openvpn;

- if you already have generated dh2048.pem file skip this step, if not run;

        openssl dhparam -out dh2048.pem 2048
        
- next open your ss config file, /etc/openvpn/server_ss.conf;

        - now config your ports, static ip from client side ss, route and ip's for both ends of the tunel, under the port line;
        
                lport 11194

                remote 35.168.119.32
                rport 11194

                ifconfig 192.168.100.100 192.168.100.101
                route 172.30.0.0 255.255.0.0
                
        - name your tunel under ;dev tap;

                ;dev tap
                dev-type tun
                dev tun-ss
        
        - change the name of .crt and .key files;

                ca ca.crt
                cert chained.crt
                key ivpn.key 
        
        - comment this two next lines;

                ;server 10.8.0.0 255.255.255.0
                
                ;ifconfig-pool-persist /var/log/openvpn/ipp.txt
                               
        - edit push route line to your network ip;

                push "route 172.29.0.0 255.255.0.0"
                ;push "route 192.168.20.0 255.255.255.0"       
                
        - keep the tls-auth line with a zero for the server side config;

                tls-auth ta.key 0 # This file is secret
                
        - in the end add this following line;

                tls-server
                
        - after that save the file;

- now restart openvpn.serice and enable server_ss.conf file;

        systemctl disable openvpn.service 
        systemctl stop openvpn.service 
  
        systemctl enable openvpn@server_ss
        systemctl start openvpn@server_ss
  
        systemctl enable --now openvpn.service
       
                
    
                 
        
