#Remote access client side (client.conf)


- install openvpn;

        apt install openvpn -y
        
- place ca.crt, chained.crt, cli.key & ta.key(generated on) inside /etc/openvpn;

        chmod 600 cli.key


- next open /etc/openvpn/cli.conf;

        - change "my-server-1" to the static ip of the server;
                
                remote x.x.x.x 1194
                ;remote my-server-2 1194

        - next change the name of the .crt and .key files;
        
                ca ca.crt
                cert chained.crt
                key cli.key                               
                
        - now just save file;
        

- now restart openvpn.serice and enable client.conf file;

        systemctl disable openvpn.service 
        systemctl stop openvpn.service 
        
        systemctl enable openvpn@client
        systemctl start openvpn@client
        
        systemctl enable --now openvpn.service
