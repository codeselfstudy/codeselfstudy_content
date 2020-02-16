---
title: How to Programatically Invite People to Slack Chatrooms
date: 2016-04-24
author: Josh
path: "/blog/how-to-programatically-invite-people-to-slack-chatrooms/"
---

There are scripts that one can use (like <a href="https://github.com/rauchg/slackin">Slakin</a>) that let you create user registration forms for Slack. I was poking around in the Slakin code and the Slack API and I extracted the part that actually invites the users. You can use this code to create your own custom invite tools for Slack.

Here is an example of how to invite a user to Slack with Python 3:

```python
import requests
from datetime import datetime

o = 'myslacksubdomain'  # Organization
t = '*********'  # API token
e = 'user@example.com'  # Email
c = 'C04H3KVI5'  # Channel IDs. I think this can be a comma-separated string of channels
# e.g., invite(o, t, e, c)

base_url = 'https://{}.slack.com/api'.format(o)

def invite(org, token, email, channel):
    """Invite a user to your Slack org."""
    ts = int(datetime.now().timestamp())
    url = '{}/users.admin.invite?t={}'.format(base_url, org, ts)
    payload = {
        'email': email,
        'token': token,
        'channels': channel,
        'set_active': True
    }
    headers = {
        'cache-control': "no-cache"
    }

    print('About to send payload: {}'.format(payload))
    print('to: {}'.format(url))

    res = requests.request('POST', url, headers=headers, params=payload)

    # See what gets sent back
    print('Got: {}'.format(res.status_code))
    print(res.text)
```

If you have questions, leave a comment below.
