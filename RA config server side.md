#Remote Access Server side (Server_ra.conf)


- install openvpn;
        
        apt install openvpn -y

- place ca.crt, chained.crt & ivpn.key inside /etc/openvpn;

        chmod 600 ivpn.key
        
- next open /etc/openvpn/server_ra.conf;

        - change the names of de .crt and .key files;
                
                # (see "pkcs12" directive in man page).
                ca ca.crt
                cert chained.crt
                key ivpn.key  # This file should be kept secret


        - press ctrl z and run;
                
                openssl dhparam -out dh2048.pem 2048
                
        - type fg to go back to your suspended file, then edit the subnet address to assign to clients;
        
                server 10.8.0.0 255.255.255.0 - in my case i left the default one 
        
        - next edit push routes;
                
                push "route 172.31.0.0 255.255.0.0"
        
        - then go again to cmd line and run;
                
                openvpn --genkey --secret ta.key - to genarate a ta.key file
        
        - after that just save file;
                
                
- now restart openvpn.serice and enable server_ra.conf file;

        systemctl disable openvpn.service 
        systemctl stop openvpn.service 
        
        systemctl enable openvpn@server_ra
        systemctl start openvpn@server_ra
        
        systemctl enable --now openvpn.service
                
                

 
                
