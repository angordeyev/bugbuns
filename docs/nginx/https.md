# Setup HTTPS using Certbot

The example uses Debian.

## Prerequisites

Add A record for the subdomain.


Install NGINX and Certbot:

```bash
# Install NIGNX
sudo apt-get update
sudo apt-get -y install nginx

## Install Certbot
sudo apt-get -y install certbot
sudo apt-get install python3-certbot-nginx
```

## Generate a Certificate

```bash
sudo certbot --nginx -d subdomain.domain.com
```

```output
...
Successfully received certificate.
Certificate is saved at: /etc/letsencrypt/live/some.bugbuns.com/fullchain.pem
Key is saved at:         /etc/letsencrypt/live/some.bugbuns.com/privkey.pem
...
These files will be updated when the certificate renews.
Certbot has set up a scheduled task to automatically renew this certificate in the background.
...
```

Certbot will generate the cron task:

```bash title="/etc/cron.d/certbot"
# /etc/cron.d/certbot: crontab entries for the certbot package
#
# Upstream recommends attempting renewal twice a day
#
# Eventually, this will be an opportunity to validate certificates
# haven't been revoked, etc.  Renewal will only occur if expiration
# is within 30 days.
#
# Important Note!  This cronjob will NOT be executed if you are
# running systemd as your init system.  If you are running systemd,
# the cronjob.timer function takes precedence over this cronjob.  For
# more details, see the systemd.timer manpage, or use systemctl show
# certbot.timer.
SHELL=/bin/sh
PATH=/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin

0 */12 * * * root test -x /usr/bin/certbot -a \! -d /run/systemd/system && perl -e 'sleep int(rand(43200))' && certbot -q renew --no-random-sleep-on-renew
```
