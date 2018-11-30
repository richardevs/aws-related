# AWS Lambda Python 3.6

import json
from botocore.vendored import requests

def lambda_handler(event, context):
    import boto3
    client = boto3.client('ec2')
    
    response = client.describe_instances(
        Filters=[
            {
                'Name': 'instance-state-name',
                        'Values': [
                            'running'
                        ]
            },
        ],
    )
    
    if response['Reservations']:
        WEB_HOOK_URL = "" # Insert your Slack Webhook URL in the quote
        requests.post(WEB_HOOK_URL, data = json.dumps({
            'text': u'*Staging environments are still running!*',
            'username': u'ALERTS FROM AWS',
            'icon_emoji': u':u_nya:',
            'link_names': 0,
        }))
    else:
        print("No instances are running.")
