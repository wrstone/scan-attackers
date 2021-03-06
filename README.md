# scan-attackers

This is a Bash script that launches an nmap "Slow comprehensive scan" against IP addresses identified as attack nodes by Fail2Ban (http://www.fail2ban.org).

It reads a list of IP addresses from a text file containing one IP address on each line.

It will then save the scan output to a file for later review.

This script intended to be run inside a GNU screen (https://www.gnu.org/software/screen/) session so that it may run detached.

-----

Known Issues:

1.  It's running a slow, methodical scan.  It takes a _long_ time to run.  Investigate other scans that will reliably return the required data in a reasonable period of time.

2.  It can't be gracefully shut down and started up again. The script will always start at the top of the list.  It should remove half-finished scans on shutdown; it should continue where it left off on startup.

3.  It needs to be able to obtain IP addresses more dynamically.  At present the IP list is manually-generated.  The script should obtain the addresses from Fail2Ban or iptables (which are used to create the attack node database); or via a dynamically-updated file.

4.  nmap didn't recover when the network Internet connection flapped, which required killing the script.  Investigate means to force nmap to halt and then restart scans that takes too long to complete.  Possibly resolved by (1) above.
