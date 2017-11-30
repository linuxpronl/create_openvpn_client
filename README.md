Create OpenVPN client configuration

Intro

I created this script to make it easier to create OpenVPN ovpn configuration files. 

This script is tested on Fedora Linux, OpenVPN 2.3.x and Easy-RSA 2.2.x but should work on RedHat and CentOS as well. 
It's not tested on Ubuntu, other Debian derivates and SuSE. 

The script can also be used to create the client key and certificate or you can skip this step and just create a configuration file with existing cert's and key's. 

Since TLS-AUTH is strongly recommended, the script creats a client confiuguration with tls-auth. You have to set the TLSAUTHKEY parameter pointing to the tls-auth key. 

Assumptions

Assumtions are the mother of all fuckups so lets mention them: 
- assuming you have a working OpenVPN server configuration preferably with TLS-AUTH
- assuming you have (basic) Linux knowlegde 


Config

First configure create-client, it's rather straight forward. You might want to take
attention to read/write rights to the OUTDIR so the script is able to write te configuration file. 

If you want to enable tls-auth (and you want this), create a server key using:

   openvpn --genkey --secret ta.key 

and add the following lines to your server config and restart OpenVPN

   key server.key  
   tls-auth ta.key 0

The script will add the appropriate lines to the client configuration file. 


Usage

After configuring create-client you can run it with: 

./create-config <clientname>  

It perform some checks and will on success create a <clientname>.ovpn configuration file
in the given outdir. 


