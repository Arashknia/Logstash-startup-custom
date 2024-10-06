# Building a new instance of logstash
1. **First you need to take a copy from the current stable configuration to the new one (for example logstash 2):**
   ```
   cp –rp /etc/logstash /etc/logstash2
   ```
2. **You have to change the configuration of some files like below:**
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
