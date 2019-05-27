# ansible-aws-cloudwatch-agent-config
Configure amazon-cloudwatch-agent to stream logfiles to Cloudwatch dashboard.

## Requirements ##
- amazon-cloudwatch-agent installed. Role: https://github.com/traveloka/ansible-aws-cloudwatch-agent
- amazon-ssm installed

## Role Variable ##

     - name: aws_cwa_config_name
       desc: name of the configuration file
   
     - name: aws_cwa_logfiles
       desc: list of log configuration settings to be placed into a single config file:
       
       - name: file_path
         desc: Specifies the path of the log file to upload to CloudWatch Logs.
       
       - name: log_group_name
         desc: Specifies what to use as the log group name in CloudWatch Logs.
         
       - name: log_stream_name
         desc: Optional. Specifies what to use as the log stream name in CloudWatch Logs.
         default: {hostname}
      
       - name: timestamp_format
         desc: Optional. Specifies the timestamp format, using plaintext and special symbols that start with %. If you omit this field, the current time is used
         
       - name: timezone
         desc:  Optional. Specifies the time zone to use when putting timestamps on log events. The valid values are UTC and Local.
         default: Local
       
       - name: multi_line_start_pattern
         desc: Specifies the pattern for identifying the start of a log message. A log message is made of a line that matches the pattern and any subsequent lines that don't match the pattern. 
         
       - name: encoding
         desc: Specified the encoding of the log file so that it can be read correctly. If you specify an incorrect coding, there might be data loss because characters that can't be decoded are replaced with other characters.
         default: utf-8
    
### defaults ###

    - name: aws_cwa_dest_path
      desc: Destination path where amazon-cloudwatch-agent installed
      value: /opt/aws/amazon-cloudwatch-agent

    - name: aws_cwa_logfile_path
      desc: Path where amazon-cloudwatch-agent write the log
      value: /opt/aws/amazon-cloudwatch-agent/logs/amazon-cloudwatch-agent.log
      
    - name: aws_region
      desc: Region where parameter store uploaded
      value: ap-southeast-1
      
## Dependencies ##

None

## Example Playbook ##

    - hosts: servers
      roles:
        - role: ansible-aws-cloudwatch-agent-config
          aws_cwa_config_name: "tsi-cwa-config"
          aws_cwa_logfiles:
             - file_path: "/var/log/syslog"
               log_group_name: "/tvlk/test/syslog.log"
               timestamp_format: "%b %d %H:%M:%S"
               timezone: "UTC"


    
