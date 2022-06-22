Exercise: Sending Alert Messages
Configure AlertManager to notify of a critical error.

Instructions:
Open port 9093 to traffic in the security groups of your EC2 instance.
SSH into your Prometheus server (EC2 instance from the previous exercise)
Follow the instructions in this tutorial to set up Alertmanager and alerting rules for Prometheus.
https://codewizardly.com/prometheus-on-aws-ec2-part4/

Set up a "receiver" for Slack, Pager Duty, or email using Gmail (or your own SMTP server).
Restart the server and you should see an alert!

open alertmanager.yml and edit:
nano alertmanager.yml

replace the content with:

global:
    resolve_timeout: 1m
    slack_api_url: 'https://hooks.slack.com/services/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'

route:
    receiver: 'slack-notifications'

receivers:
    - name: 'slack-notifications'
        slack_configs:

        -   channel: '#hugb'
            send_resolved: true


save and exit: ctr x, Y, then ENTER

Your Monitoring System Has a Voice!
Monitoring is not much without alerting. Having metrics is good, but predicting problems before they exist is powerful! That being said, be careful with alert fatigue and desensitization and consider where to alert and who should see it. Maybe experiment with other receiver types as you work on your alerting systems.

https://prometheus.io/docs/prometheus/latest/querying/basics/