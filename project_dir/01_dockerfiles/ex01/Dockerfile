FROM debian
MAINTAINER skholodn@student.unit.ua
RUN apt update && apt install -y wget bzip2 && cd /tmp && \
	wget http://dl.4players.de/ts/releases/3.0.13.8/teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2 && \
	tar -xf teamspeak3-server_linux_amd64-3.0.13.8.tar.bz2 && \
	mkdir /opt/teamspeak && mv teamspeak3-server_linux_amd64 /opt/teamspeak/. && \
	mkdir -p /opt/teamspeak/data/logs && mkdir -p /opt/teamspeak/data/files && \
	ln -s /opt/teamspeak/data/ts3server.sqlitedb /opt/teamspeak/teamspeak3-server_linux_amd64/ts3server.sqlitedb
ENTRYPOINT ["/opt/teamspeak/teamspeak3-server_linux_amd64/ts3server_minimal_runscript.sh"]
CMD ["inifile=/opt/teamspeak/data/ts3server.ini", \
"logpath=/opt/teamspeak/data/logs","licensepath=/opt/teamspeak/data/", \
"query_ip_whitelist=/opt/teamspeak/data/query_ip_whitelist.txt", \
"query_ip_backlist=/opt/teamspeak/data/query_ip_blacklist.txt", "start;"]
VOLUME ["/opt/teamspeak/data"]
EXPOSE 9987/udp 30033 10011
