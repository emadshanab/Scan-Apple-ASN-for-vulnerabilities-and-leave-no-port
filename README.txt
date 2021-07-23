Scan Apple ASN for vulnerabilities and leave no port:-

We will use multiple programs to scan all ports and sort them and finally Nuclei will find CVES and high vulnerabilities for us:-

Install the following programs and add alias on your .bashrc file or .zshrc file:-

https://github.com/projectdiscovery/mapcidr
https://github.com/projectdiscovery/nuclei
https://github.com/projectdiscovery/nuclei-templates
https://github.com/emadshanab/Nuclei-Templates-Collection
https://github.com/projectdiscovery/httpx
https://github.com/projectdiscovery/naabu
https://github.com/tomnomnom/httprobe
https://github.com/tomnomnom/anew
https://github.com/j3ssie/metabigor
https://github.com/nmap/nmap
https://github.com/robertdavidgraham/masscan
--------------------------------------------------------------------------------------------------------------------

To install them use this commands on your terminal:-

GO111MODULE=on go get -v github.com/projectdiscovery/mapcidr/cmd/mapcidr
GO111MODULE=on go get -v github.com/projectdiscovery/nuclei/v2/cmd/nuclei
GO111MODULE=on go get -v github.com/projectdiscovery/httpx/cmd/httpx
GO111MODULE=on go get -v github.com/projectdiscovery/naabu/v2/cmd/naabu
GO111MODULE=on go get github.com/j3ssie/metabigor
go get -u github.com/tomnomnom/httprobe
go get -u github.com/tomnomnom/anew
apt-get install nmap
apt-get install masscan

Now will make an alias to all programs to avoid any errors ( i prefer the manual way) add these lines on .bashrc file or .zshrc file and save it.

alias mapcidr='/root/go/bin/mapcidr'
alias nuclei='/root/go/bin/nuclei'
alias httpx='/root/go/bin/httpx'
alias naabu='/root/go/bin/naabu'
alias anew='/root/go/bin/anew'
alias metabigor='/root/go/bin/metabigor'
--------------------------------------------------------------------------------------------------------------------
Now you are ready to go:-

You can use metabigor to find the ASN for you and save the result:-

The command is:-

echo "apple" | metabigor net --org -o /root/apple_asn.txt

You can replace the company name like facebook,twitter,microsoft,netflix,yahoo
--------------------------------------------------------------------------------------------------------------------
1:- I have uploaded the ASN to my github repo you can download it and save it as apple_asn.txt

https://github.com/emadshanab/apple-ASN

First will slice the ASN to ips via mapcidr

mapcidr -l apple_asn.txt -o apple_asn_output.txt 

Now will scan the apple_asn_output.txt file via multiple programs and please use your VPS to avoid any losing of your internet traffic on your home network.
--------------------------------------------------------------------------------------------------------------------

1:- via httprobe will use the xlarg option and it will scan for these ports,check the source code of httprobe

https://github.com/tomnomnom/httprobe/blob/master/main.go

xlarge := []string{"81", "300", "591", "593", "832", "981", "1010", "1311", "2082", "2087", "2095", "2096", "2480", "3000", "3128", "3333", "4243", "4567", "4711", "4712", "4993", "5000", "5104", "5108", "5800", "6543", "7000", "7396", "7474", "8000", "8001", "8008", "8014", "8042", "8069", "8080", "8081", "8088", "8090", "8091", "8118", "8123", "8172", "8222", "8243", "8280", "8281", "8333", "8443", "8500", "8834", "8880", "8888", "8983", "9000", "9043", "9060", "9080", "9090", "9091", "9200", "9443", "9800", "9981", "12443", "16080", "18091", "18092", "20720", "28017"}

The command is:- 

cat apple_asn_output.txt | httprobe -c 100 -t 20000 -p xlarge >apple_asn_httprobexlarg.txt
--------------------------------------------------------------------------------------------------------------------

2:- via httprobe with specific ports of our choice:-

The command is:-

cat apple_asn_output.txt | httprobe -p http:81 -p http:300- p http:591 -p http:593 -p http:832 -p http:981 -p http:1010 -p http:1311 -p http:2082 -p http:2087 -p http:2095 -p http:2096 -p http:2480 -p http:3000 -p http:3128 -p http:3333 -p http:4243 -p http:4567 -p http:4711 -p http:4712 -p http:4993 -p http:5000 -p http:5104 -p http:5108 -p http:5800 -p http:6543 -p http:7000 -p http:7396 -p http:7474 -p http:8000 -p http:8001 -p http:8008 -p http:8014 -p http:8042 -p http:8069 -p http:8080 -p http:8081 -p http:8088 -p http:8090 -p http:8091 -p http:8118 -p http:8123 -p http:8172 -p http:8222 -p http:8243 -p http:8280 -p http:8281 -p http:8333 -p http:8443 -p http:8500 -p http:8834 -p http:8880 -p http:8888 -p http:8983 -p http:9000 -p http:9043 -p http:9060 -p http:9080 -p http:9090 -p http:9091 -p http:9200 -p http:9443 -p http:9800 -p http:9981 -p http:12443 -p http:16080 -p http:18091 -p http:18092 -p http:20720 -p http:28017 -p http:8009 -p http:8180 -p https:81 -p https:300- p https:591 -p https:593 -p https:832 -p https:981 -p https:1010 -p https:1311 -p https:2082 -p https:2087 -p https:2095 -p https:2096 -p https:2480 -p https:3000 -p https:3128 -p https:3333 -p https:4243 -p https:4567 -p https:4711 -p https:4712 -p https:4993 -p https:5000 -p https:5104 -p https:5108 -p https:5800 -p https:6543 -p https:7000 -p https:7396 -p https:7474 -p https:8000 -p https:8001 -p https:8008 -p https:8014 -p https:8042 -p https:8069 -p https:8080 -p https:8081 -p https:8088 -p https:8090 -p https:8091 -p https:8118 -p https:8123 -p https:8172 -p https:8222 -p https:8243 -p https:8280 -p https:8281 -p https:8333 -p https:8443 -p https:8500 -p https:8834 -p https:8880 -p https:8888 -p https:8983 -p https:9000 -p https:9043 -p https:9060 -p https:9080 -p https:9090 -p https:9091 -p https:9200 -p https:9443 -p https:9800 -p https:9981 -p https:12443 -p https:16080 -p https:18091 -p https:18092 -p https:20720 -p https:28017 -p https:8009 -p https:8180 -c 50 | tee apple_asn_httprobe_specific.txt
--------------------------------------------------------------------------------------------------------------------
3:- Via httpx :-

The command is:-

httpx -l apple_asn_output.txt -ports 81,300,591,593,832,981,1010,1311,2082,2087,2095,2096,2480,3000,3128,3333,4243,4567,4711,4712,4993,5000,5104,5108,5800,6543,7000,7396,7474,8000,8001,8008,8014,8042,8069,8080,8081,8088,8090,8091,8118,8123,8172,8222,8243,8280,8281,8333,8443,8500,8834,8880,8888,8983,9000,9043,9060,9080,9090,9091,9200,9443,9800,9981,12443,16080,18091,18092,20720,28017,8009,8180 -threads 200 | anew apple_asn_httpx.txt

4:- Via httpx and will scan for all ports:-

The command is:-
httpx -l apple_asn_output.txt  -t 100 -ports 1-65535 -o apple_asn_httpx_allports.txt

--------------------------------------------------------------------------------------------------------------------
5:- Via naabu:-

The command is:-

naabu -hL apple_asn_output.txt -t 100 -ports 1-65535 -verify  -o apple_asn_naabu.txt

--------------------------------------------------------------------------------------------------------------------
6:- Via nmap and masscan:-

The command is:-

nmap -sn -Pn -n -iL apple_asn_output.txt -oG out.txt | awk -F" " '{print $2}' out.txt > outnew.txt | masscan -iL outnew.txt --ports 0-65535 -oG apple_nmap_scan.txt
--------------------------------------------------------------------------------------------------------------------
6:-After all the tools finished we will collect our scan and sort it to avoid any duplicates:-

cat apple_asn_httprobexlarg.txt apple_asn_httprobe_specific.txt apple_asn_httpx.txt apple_asn_httpx_allports.txt apple_asn_naabu.txt apple_nmap_scan.txt | sort -u | anew apple_final.txt
--------------------------------------------------------------------------------------------------------------------
7:- Finally will scan the outfile apple_final.txt via nuclei:-

The command is:- 

nuclei -c 500 -l apple_final.txt -t /root/nuclei-templates/ -severity critical,high,medium -o apple_nuclei_results.txt


Good luck!

Emad Shanab - أبو عبد الله

@Alra3ees
