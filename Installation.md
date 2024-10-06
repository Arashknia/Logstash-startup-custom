# Offline installation
1. * Download Logstash latest version or 8.15.2 .deb *[logstash-8-15-2.deb](https://www.elastic.co/downloads/past-releases/logstash-8-15-2)*
2. * install it on your Ubuntu Linux with > ```sudo dpkg -i <downloaded package>```
3. * enter these commands:
   > ```
   > systemctl daemon-reload
   > systemctl enable logstash
   > ```
4. put or create your config file based on what you need on `/etc/logstash/conf.d/(your-config).conf`
5. if you have installed a new Ubuntu, enter these commands to make logstash available for logging:
   > ```
   > systemctl enable rsyslog
   > systemctl start rsyslog
   > ```
   
7. if your configuration contains Syslog as output or input (sending or receiving log by syslog protocol), you have to install the <b>*logstash-output-syslog*</b> plugin on your logstash:

   for online installation:
   > ```
   > sudo /usr/share/logstash/bin/logstash-plugin install logstash-output-syslog
   > ```

   HINT: (if you are getting socket error, enter the command multiple times)

# Configurations
1. <b>logstash.yaml:</b> `(/etc/logstash/logstash.yaml)`
* change or set these configurations: (uncomment them if they exist and then enter the correct value)

  > node.name: logstash
  
  > path.data: /var/lib/logstash

  > path.config: /etc/logstash/conf.d/*.conf

  > path.logs: /var/log/logstash

2. <b>startup.options</b> `(/etc/logstash/startup.options)`
* change or set these configurations: (uncomment them if they exist and then enter the correct value)

  > LS_SETTINGS_DIR=/etc/logstash
  
  > SERVICE_NAME="logstash"
  
  > SERVICE_DESCRIPTION="logstash"

3. <b>log4j2.properties</b>:
* change or set these configurations: (uncomment them if they exist and then enter the correct value)

  > appender.rolling.fileName = /var/log/logstash/logstash-main.log
  
  > appender.rolling.filePattern = /var/log/logstash/logstash-main-%d{yyyy-MM-dd}-%i.log.gz

  > appender.rolling.strategy.action.condition.glob = logstash*

4. <b>/etc/logstash/pipelines.yml</b>
  > COMMENT EVERYTHING WITHIN THIS FILE
