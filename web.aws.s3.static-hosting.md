# Setup Static Content Hosting On Amazon S3

[aws.amazon.com](https://s3.console.aws.amazon.com/s3/home)

## Setting Up S3 Bucket

*Use a simple naming convention to match domain or subdomain.*

1; Create Bucket
    - Bucket name: sub.domain.tld
    - Region: {varies}
    - Uncheck Block all public access and acknowledge that the current settings will provide public access to this bucket.

2; Configure Public Access To Bucket
    - Click on bucket name and navigate to permissions.
    - Scroll down and edit the Bucket policy.

     ```yaml
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "PublicReadGetObject",
          "Effect": "Allow",
          "Principal": "*",
          "Action": "s3:GetObject",
          "Resource": "BUCKET_ARN_GOES_HERE/*",
          "Condition": {
            "IpAddress": {
              "aws:SourceIp": [
                "2400:cb00::/32",
                "2405:8100::/32",
                "2405:b500::/32",
                "2606:4700::/32",
                "2803:f800::/32",
                "2c0f:f248::/32",
                "2a06:98c0::/29",
                "103.21.244.0/22",
                "103.22.200.0/22",
                "103.31.4.0/22",
                "104.16.0.0/12",
                "108.162.192.0/18",
                "131.0.72.0/22",
                "141.101.64.0/18",
                "162.158.0.0/15",
                "172.64.0.0/13",
                "173.245.48.0/20",
                "188.114.96.0/20",
                "190.93.240.0/20",
                "197.234.240.0/22",
                "198.41.128.0/17"
              ]
            }
          }
        }
      ]
    }
  ```
      - Save changes.

3; Setup Static Website Hosting
    - Click on bucket name and navigate to properties.
    - Scroll down and edit the Static website hosting settings.
        - Static website hosting: Enable
        - Index document: index.html
        - Error document: 404.html
    - Save changes.
    - Access on the S3 Dashboard should now read Public.

## Setup Remote Access to S3 Bucket

1. Open IAM in Amazon Web Services Dashboard.
2. On the right, locate Quick Links > My access key
3. Create New Access Key if needed. Download a copy if needed.
4. Configure desired application for access:

> Protocol: S3
> Server: s3.amazonaws.com
> Access Key ID: `ACCESS_KEY_ID`
> Secret: `SECRET`

You can create a new IAM user if needed to restrict access to each S3 bucket on your account if needed.
