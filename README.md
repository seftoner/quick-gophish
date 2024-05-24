# quick-gophish

❗️ This is fork of [pca-gophish-composition](https://github.com/cisagov/pca-gophish-composition) ❗️

Creates a Docker composition containing instances of:

- [gophish](https://github.com/gophish/gophish/) phishing framework v0.12.1.
- [mailhog](https://github.com/mailhog/MailHog) email testing tool.
- postfix mail server.

To start the composition use the command: `sudo docker-compose up --build`

Connect to the `gophish` admin web interface at:
[https://localhost:3333](https://localhost:3333).
The default credentials are `admin`, `gophish`.

Once the composition is running, `gophish` will need to be
configured to talk to `mailhog` and `postfix`. Create new
sending profiles for the two servers as listed below:

| Name    | Host:Port    |
| ------- | ------------ |
| MailHog | mailhog:1025 |
| Postfix | postfix:587  |

The `mailhog` email testing tool can be accessed at [http://localhost:8025](http://localhost:8025)


⚠️ **NOTE**:  Do not use the sample certificates in a production environment.
They are included to simplify testing.

### Ports ###

This composition exposes the following ports to the localhost:

- 1025: `postfix SMTP`
- 1587: `postfix submission`
- [3333](https://localhost:3333): `gophish admin server`
- [3380](http://localhost:3380): `gophish phish server`
- [8025](http://localhost:8025): `mailhog web interface`

### Environment Variables ###

- postfix
  - `PRIMARY_DOMAIN`: the domain of the mail server
  - `RELAY_IP`: (optional) an IP address that is allowed to relay mail without authentication

### Secrets ###

- gophish
  - `config.json`: gophish configuration file
  - `admin_fullchain.pem`: public key for admin port
  - `admin_privkey.pem`: private key for admin port
  - `phish_fullchain.pem`: public key for phishing port
  - `phish_privkey.pem`: private key for phishing port
- postfix
  - `fullchain.pem`: public key
  - `privkey.pem`: private key
  - `users.txt`: account credentials

### Volumes ###

None.