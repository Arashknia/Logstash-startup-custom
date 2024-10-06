# **Offline installation**
1. Download Logstash latest version or 8.15.2 .deb *[logstash-8-15-2.deb](https://www.elastic.co/downloads/past-releases/logstash-8-15-2)*
2. install it on your Ubuntu Linux with
   > ```
   > sudo dpkg -i <downloaded package>
   > ```
4. enter these commands:
   > ```
   > systemctl daemon-reload
   > systemctl enable logstash
   > ```
5. put or create your config file based on what you need on `/etc/logstash/conf.d/(your-config).conf`
6. if you have installed a new Ubuntu, enter these commands to make logstash available for logging:
   > ```
   > systemctl enable rsyslog
   > systemctl start rsyslog
   > ```
   
7. * if your configuration contains Syslog as output or input (sending or receiving log by syslog protocol), you have to install the <b>*logstash-output-syslog*</b> plugin on your logstash:

   for online installation:
   > ```
   > sudo /usr/share/logstash/bin/logstash-plugin install logstash-output-syslog
   > ```

   HINT: (if you are getting socket error, enter the command multiple times)

# **Configurations**

* **logstash.yml `(/etc/logstash/logstash.yml)`**
   ---
   change or set these configurations: (uncomment them if they exist and then enter the correct value)
      
   > node.name: logstash
   
   > path.data: /var/lib/logstash
   
   > path.config: /etc/logstash/conf.d/*.conf
   
   > path.logs: /var/log/logstash

* **startup.options `(/etc/logstash/startup.options)`**
   ---
   change or set these configurations: (uncomment them if they exist and then enter the correct value)
      
   > LS_SETTINGS_DIR=/etc/logstash
   
   > SERVICE_NAME="logstash"
   
   > SERVICE_DESCRIPTION="logstash"

* **log4j2.properties `(/etc/logstash/log4j2.properties)`**
   ---
   change or set these configurations: (uncomment them if they exist and then enter the correct value)
         
   > name = LogstashPropertiesConfig 
   
   > appender.rolling.fileName = /var/log/logstash/logstash-main.log
   
   > appender.rolling.filePattern = /var/log/logstash/logstash-main-%d{yyyy-MM-dd}-%i.log.gz
   
   > appender.rolling.strategy.action.condition.glob = logstash*

* **pipelines.yml `(/etc/logstash/pipelines.yml)`**
   ---
      
   > COMMENT EVERYTHING WITHIN THIS FILE

* **Enter these commands to make the change effects:**
   ---
   
   > ```
   > /usr/share/logstash/bin/system-install /etc/logstash/startup.options
   > ```
   > ```
   > systemctl enable logstash
   > systemctl start logstash
   > ```

* **Check logstash logs:**
   ---
   
   > ```
   > tail -f /var/log/logstash/logstash-main.log
   > ```
    
# Building a new instance of logstash
1. **First you need to take a copy from the current stable configuration to the new one (for example logstash 2):**
   ```
   cp –rp /etc/logstash /etc/logstash2
   ```
1. **You have to change the configuration of some files like below:**
   * **startup.options `(/etc/logstash2/startup.options)`** - change or set below configurations:
     
     > LS_SETTINGS_DIR=/etc/logstash2
  
     > SERVICE_NAME="logstash2"
  
     > SERVICE_DESCRIPTION="logstash2"

   * **logstash.yml `(/etc/logstash/logstash.yml)** - change or set below configurations:
  
     > node.name: logstash2
  
     > path.data: /var/lib/logstash2

     > path.config: /etc/logstash2/conf.d/*.conf

     > path.logs: /var/log/logstash

   * **log4j2.properties `(/etc/logstash2/log4j2.properties)`** - change or set below configurations:

     > name = Logstash2PropertiesConfig  

     > appender.rolling.fileName = /var/log/logstash/logstash2.log
  
     > appender.rolling.filePattern = /var/log/logstash/logstash2-%d{yyyy-MM-dd}-%i.log.gz

     > appender.rolling.strategy.action.condition.glob = logstash*

   * **pipelines.yml `(/etc/logstash/pipelines.yml)`**
     > COMMENT EVERYTHING WITHIN THIS FILE

3. **Enter this comment to make the change effect:**
   ```
   /usr/share/logstash/bin/system-install /etc/logstash2/startup.options
   ```
   ```
   systemctl enable logstash2
   systemctl start logstash2
   ```

6. check logstash logs:
   ```
   tail -f /var/log/logstash/logstash2.log
   ```
