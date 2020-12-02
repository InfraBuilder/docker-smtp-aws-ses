# infrabuilder/smtp-aws-ses
This docker image ([infrabuilder/smtp-aws-ses](https://hub.docker.com/r/infrabuilder/smtp-aws-ses)) is a SMTP relay built for AWS SES (but not limited to).

## Available ENV variables and their default values

| Variable               | Defaul value                            | Description                                                  |
| ---------------------- | --------------------------------------- | ------------------------------------------------------------ |
| ACCEPTED_NETWORKS      | 192.168.0.0/16 172.16.0.0/12 10.0.0.0/8 | Network who can send email through this SMTP relay           |
| RELAY_HOST             | email-smtp.us-east-1.amazonaws.com      | SMTP relay host                                              |
| RELAY_PORT             | 25                                      | SMTP relay port (should be 25, 465 or 587)                   |
| RELAY_LOGIN            | *none*                                  | Username used in SASL authentication                         |
| RELAY_PASSWORD         | *none*                                  | Password used in SASL authentication                         |
| RECIPIENT_RESTRICTIONS | *none*                                  | See http://www.postfix.org/postconf.5.html#smtpd_recipient_restrictions |
| USE_TLS                | yes                                     | Enable TLS with SMTP relay (yes or no)                       |
| TLS_VERIFY             | may                                     | See http://www.postfix.org/postconf.5.html#smtp_tls_security_level |

## Run examples

Minimal example for AWS SES in region eu-west-3 (Paris, France) : 

```bash
docker run -d --name smtp -p 25:25  \
    -e RELAY_HOST="email-smtp.eu-west-3.amazonaws.com" \
    -e RELAY_LOGIN="AWSLOGINHERE" \
    -e RELAY_PASSWORD="AWSLOGINSECRETKEY" \
    infrabuilder/smtp-aws-ses
```
## Kubernetes example

Here is an example of simple deployment with a configMap and a secret : [kubernetes/example.yaml](kubernetes/example.yaml)

## Docker image that inspired this one

Thanks to [shamil](https://github.com/shamil)

https://github.com/shamil/docker-postfix-relay