# lets-encrypt-tlsa

Learn more about this script at the [Flipping Binary website](https://flippingbinary.com)

## Installation

Modify these steps and the scripts as necessary for your distribution. The steps have been tested only on Ubuntu 16.04 servers.

1. Edit each file starting with `letsencrypt-` and change the EMAIL variable in `letsencrypt-request` to an address you can receive expiration warnings at.

2. Change the `MAIN_PATH` in each of the scripts if you want to use `/etc/letsencrypt` instead of `/etc/ssl/letsencrypt`

3. Copy `letsencrypt-autorun` to `/etc/cron.monthly` and the rest to `/usr/local/sbin`

    sudo cp letsencrypt-* /usr/local/bin
    sudo cp letsencrypt-autorun /etc/cron.monthly

You can safely copy `letsencrypt-autorun` to `/usr/local/bin` as shown above, or omit it if you wish.
