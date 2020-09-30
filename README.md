# lets-encrypt-tlsa

Read the [article](https://flippingbinary.com/2018/02/26/lets-encrypt-with-tlsa-dane/) about this script on the [Flipping Binary website](https://flippingbinary.com).

## Contributors wanted

I've noticed an uptick in interest recently, but my time is devoted to other projects at the moment. If you make improvements that you want to share, please submit a pull request. I will probably approve it as long as it doesn't break anything and provides some sort of improvement.

## Installation

Modify these steps and the scripts as necessary for your distribution. The steps have been tested only on Ubuntu 16.04 servers.

1. Change ownership and permissions of the script files

```
  $ sudo chown root:root letsencrypt-*
  $ sudo chmod +x letsencrypt-*
```

2. Change the settings in `letsencrypt-tlsa` file, especially the `EMAIL` setting!
```
  $ sudo nano letsencrypt-tlsa
```
3. Move the `letsencrypt-tlsa` file to `/etc/default` so it is accessible by the other scripts and easy to edit.
```
  $ sudo mv letsencrypt-tlsa /etc/default
```
4. Move `letsencrypt-autorun` to `/etc/cron.weekly`
```
  $ sudo mv letsencrypt-autorun /etc/cron.weekly
```
5. Move the rest to `/usr/local/sbin`
```
  $ sudo mv letsencrypt-* /usr/local/bin
```
## Usage

1. Generate a key pair and Certificate Signing Request (CSR). This script does not limit the number of domain names, but attempting to generate one certificate for dozens of domains at a time might fail. The first listed domain is primary and needs to be listed first for each command in this set of tools. Using `example.com` and `www.example.com` as an example:
```
  $ sudo letsencrypt-generate example.com www.example.com
```
2. Request a signature from Let's Encrypt. Using `example.com` and `www.example.com` as an example both of these commands do the same thing (note the primary domain is listed first and is the only one that matters):
```
  $ sudo letsencrypt-request example.com
  $ sudo letsencrypt-request example.com www.example.com
```
3. Check the hash of the signed certificate. You can list secondary domains along with the primary domain, but the hash will be the same for each. The important part includes and follows the `3 1 1` which makes up your TLSA record. Using `example.com` and `www.example.com` as an example:
```
  $ sudo letsencrypt-hash example.com www.example.com
```
4. Publish the TLSA records with your DNS provider.

5. Install the new certificates. This command will create a symlink in a consistent location (defaulting to `/etc/ssl/letsencrypt/live/<domainname>`) to the latest signed certificate for the primary domain. Using `example.com` and `www.example.com` as an example, both of these commands do the same thing (note the primary domain is listed first and is the only one that matters):
```
  $ sudo letsencrypt-install example.com
  $ sudo letsencrypt-install example.com www.example.com
```
