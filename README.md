# lets-encrypt-tlsa

Learn more about this script at the [Flipping Binary website](https://flippingbinary.com)

## Installation

Modify these steps and the scripts as necessary for your distribution. The steps have been tested only on Ubuntu 16.04 servers.

1. Change ownership and permissions of the script files

    sudo chown root:root letsencrypt-*
    sudo chmod +x letsencrypt-*

2. Change the settings in `letsencrypt-tlsa` file, especially the `EMAIL` setting!

    sudo nano letsencrypt-tlsa

3. Move the `letsencrypt-tlsa` file to `/etc/default` so it is accessible by the other scripts and easy to edit.

    sudo mv letsencrypt-tlsa /etc/default

4. Move `letsencrypt-autorun` to `/etc/cron.weekly`

    sudo mv letsencrypt-autorun /etc/cron.weekly

5. Move the rest to `/usr/local/sbin`

    sudo mv letsencrypt-* /usr/local/bin
