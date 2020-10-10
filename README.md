#Instructions to test for SquareTrade

1. cd into the project directory for bitrise-step-open-vpn. It should be the directory expanded from the zip file.
2. Install Bitrise CLI: https://devcenter.bitrise.io/bitrise-cli/installation/
3. Change ca.crt, client.crt and client.key for the correct keys to access our openvpn server. If you are running from Ubuntu and not Mac put the keys here:
/etc/openvpn/ca.crt
/etc/openvpn/client.crt
/etc/openvpn/client.key
4. Add your IP address to the whitelist of IPs that our openvpn server will accept.
5. The scripts are already configured to use our VPN server with the right AES-256-CBC
6. Run the following command from the project root directory: bitrise run test
7. If everything works you should see the ping for our server correctly in the output like this:
Configuring for Mac OS
Using AES-256-CBC
PING 10.181.75.40 (10.181.75.40): 56 data bytes
64 bytes from 10.181.75.40: icmp_seq=0 ttl=63 time=173.453 ms
64 bytes from 10.181.75.40: icmp_seq=1 ttl=63 time=20.202 ms
64 bytes from 10.181.75.40: icmp_seq=2 ttl=63 time=47.200 ms
64 bytes from 10.181.75.40: icmp_seq=3 ttl=63 time=18.698 ms
64 bytes from 10.181.75.40: icmp_seq=4 ttl=63 time=23.073 ms
64 bytes from 10.181.75.40: icmp_seq=5 ttl=63 time=19.880 ms
64 bytes from 10.181.75.40: icmp_seq=6 ttl=63 time=20.884 ms
64 bytes from 10.181.75.40: icmp_seq=7 ttl=63 time=14.992 ms
64 bytes from 10.181.75.40: icmp_seq=8 ttl=63 time=20.534 ms
64 bytes from 10.181.75.40: icmp_seq=9 ttl=63 time=16.280 ms
64 bytes from 10.181.75.40: icmp_seq=10 ttl=63 time=47.150 ms
64 bytes from 10.181.75.40: icmp_seq=11 ttl=63 time=18.187 ms

If it does not work you will see:

Configuring for Mac OS
Using AES-256-CBC
PING 10.181.75.40 (10.181.75.40): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
Request timeout for icmp_seq 3
Request timeout for icmp_seq 4
Request timeout for icmp_seq 5
Request timeout for icmp_seq 6
Request timeout for icmp_seq 7
Request timeout for icmp_seq 8

For reference the bash file we are running is step.sh and we are not using .bitrise.secrets.yml . If this work for our server, I will clean up the script to use environment variables and push the step Github to use in the web CI console.


# Connect to OpenVPN Server step

Establish a VPN connection with the specified OpenVPN server.
