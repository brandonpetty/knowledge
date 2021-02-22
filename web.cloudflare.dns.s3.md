# Configure Cloudflare for DNS

[dash.cloudflare.com](https://dash.cloudflare.com/)

## DNS Records

*Ensure that domain is pointed to Cloudflare nameservers before proceeding.*

1. Configure CNAME records for Amazon S3.
2. Verify that domain or subdomain is resolving as intended.

| Type        | Name        | Content       |  TTL  |  Proxy  |
| :---        | :----:      | :---:         | :---: |  :---:  |
| CNAME      | www       | BUCKET-NAME.s3-website-US-EAST-1.amazonaws.com   |    Auto   |    Proxied     |
| CNAME      | @       | BUCKET-NAME.s3-website-US-EAST-1.amazonaws.com   |    Auto   |    Proxied     |

## E-Mail Address, MX, and/or FastMail

1. Configure TXT and MX records for email services. If using Fast Mail add CNAME records.

| Type        | Name        | Content       |  TTL  |  Proxy  |
| :---        | :----:      | :---:         | :---: |  :---:  |
| MX      | @       |  Mail Server Address w/ Priority  |    Auto   |    DNS only     |
| MX      | @       |  Mail Server Address w/ Priority  |    Auto   |    DNS only     |
| TXT      | @       |  Content  |    Auto   |    DNS only     |
| CNAME      | fm1._domainkey      |  fm1.DOMAIN.TLD.dkim.fmhosted.com  |    Auto   |    Proxied     |
| CNAME      | fm2._domainkey      |  fm2.DOMAIN.TLD.dkim.fmhosted.com  |    Auto   |    Proxied     |
| CNAME      | fm3._domainkey      |  fm3.DOMAIN.TLD.dkim.fmhosted.com  |    Auto   |    Proxied     |

## Redirect domain.tld to www.domain.tld

1. Navigate to Page Rules and Create Page Rule.
    - If the URL matches: domain.tld/*
    - Forwarding URL: 301 - Permanent Redirect
    - `https://sub.domain.tld/$1`
2. Save settings.
