![](https://github.com/CTFd/CTFd/blob/master/CTFd/themes/core/static/img/logo.png?raw=true)
====

[![Build Status](https://travis-ci.org/CTFd/CTFd.svg?branch=master)](https://travis-ci.org/CTFd/CTFd)
[![CTFd Slack](https://slack.ctfd.io/badge.svg)](https://slack.ctfd.io/)
[![Documentation Status](https://readthedocs.org/projects/ctfd/badge/?version=latest)](https://docs.ctfd.io/en/latest/?badge=latest)

## What is CTFd?
CTFd is a Capture The Flag framework focusing on ease of use and customizability. It comes with everything you need to run a CTF and it's easy to customize with plugins and themes.

![CTFd is a CTF in a can.](https://github.com/CTFd/CTFd/blob/master/CTFd/themes/core/static/img/scoreboard.png?raw=true)

## Install

Start CTFd in a docker container, but use the local source code

`docker run -p 8000:8000 -d --restart unless-stopped --name ctfd -v /opt/CTFd:/opt/CTFd ctfd/ctfd`

Configure an apache reverse proxy

```
    # Proxy to a backend app
    ProxyRequests Off
    ProxyPreserveHost On
    ProxyAddHeaders On

    RequestHeader set X-Forwarded-Proto https

    RewriteEngine On
    RewriteCond %{HTTP:Upgrade} websocket [NC]
    RewriteRule /(.*) ws://localhost:8000/$1 [P,L]

    ProxyPass / http://localhost:8000/ retry=0 nocanon
    ProxyPassReverse / http://localhost:8000/
```

## Credits
 * Logo by [Laura Barbera](http://www.laurabb.com/)
 * Theme by [Christopher Thompson](https://github.com/breadchris)
 * Notification Sound by [Terrence Martin](https://soundcloud.com/tj-martin-composer)

## User Management

Self-managed teams have been disabled, and there is no admin UI to manage team memberships.
Use `sqlite3` to manage team membership.

`sqlite3 /opt/CTFd/CTFd/ctfd.db`

List users & teams

```sql
SELECT * FROM teams;
SELECT * FROM users;
```

Assign a user to a team

```sql
UPDATE USERS SET team_id=1 WHERE name='username';
```
