# certbot-dns-name-com

A certbot DNS plugin for `Name.com`. Supports wildcard domains.

Copy `.env.example` file to `.env` and fill with your data. For multiple domains, create a .env folder and name each .env file with the primary domain on the certificate (exampledomain.com.env, exampledomain.io.env, etc).

## Usage:

Clone project to `/usr/local` or copy files to `/usr/local/certbot-dns-name-com`, otherwise - correct paths in scripts

### New Cert using CertOnly

`$ certbot --standalone certonly --cert-name exampledomain.com --manual-auth-hook "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh add" --manual-cleanup-hook "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh clean" -d exampledomain.com -d www.exampledomain.com`

### Check
`$ certbot renew --cert-name yourdomain.com --manual-auth-hook "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh add" --manual-cleanup-hook "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh clean" --dry-run`

### Renew
`$ certbot renew --cert-name yourdomain.com --manual-auth-hook "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh add" --manual-cleanup-hook "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh clean"`

### Manually Update Renewal Configuration
If you have already installed a certificate before using this plugin, and are not yet able to renew, you can still configure the hooks for the next renewal. This is not ideal, but there is no way via the certbot commands to update this without renewing or creating a new cert.

** Note: Manually editing the renewal configuration file for your certificate is discouraged by the LetsEncrypt team. **

Ensure these properties are added to your renewal configuration. The file is found in `/etc/letsencrypt/renewal/{{certname}}.conf`
```
pref_challs = dns-01,
authenticator = manual
manual_auth_hook = "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh add"
manual_cleanup_hook = "/usr/local/certbot-dns-name-com/certbot_dns_auth.sh clean"
```


