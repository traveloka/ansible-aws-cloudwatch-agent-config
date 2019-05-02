# ansible-aws-cloudwatch-agent-config
Configure amazon-cloudwatch-agent to stream the metrics and logfile to Cloudwatch dashboard.

## Requirements ##
- amazon-cloudwatch-agent already installed

## Role Variable ##

### defaults ###

    - name: aws_cwa_dest_path
      desc: Destination path where amazon-cloudwatch-agent installed
      value: /opt/aws/amazon-cloudwatch-agent

    - name: aws_cwa_logfile_path
      desc: Path where amazon-cloudwatch-agent write it's log
      value: /opt/aws/amazon-cloudwatch-agent/logs/amazon-cloudwatch-agent.log
      
## Dependencies ##

None

## Example Playbook ##

    - hosts: servers
      roles:
        - role: ansible-aws-cloudwatch-agent-config
          aws_cwa_config_name: "MetricSyslog"
          aws_cwa_logfiles:
            - pathfile: "/var/log/syslog"
              timestamp_format: "%b %d %H:%M:%S"
              group_name: "/tvlk/global/syslog"


    
