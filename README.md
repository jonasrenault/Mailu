This fork of Mailu modifies

- the admin container to add a configuration option `WEB_SSO_PREFIX` which updates the url_path for `sso` and `static` routes served by the admin web app
- the unbound container to add a forward rule to the host DNS
- the webmail container to add custom snappymail configuration (enable plugins)
- adds labels to push these modified images to github's package container

**These modifications are in the `intellab-custom-containers` branch. First switch to this branch before building the images.**

Follow the [doc on mailu](https://mailu.io/2.0/contributors/environment.html#building-images) to build the docker images and push them to github's container registry:

- Create a token on github with write access for containers and use this token to login to github's container registry.
```console
export CR_PAT=YOUR_TOKEN
echo $CR_PAT | docker login ghcr.io -u USERNAME --password-stdin
```

- Set the `DOCKER_ORG` and `MAILU_VERSION` env vars

```console
export DOCKER_ORG="ghcr.io/jonasrenault"
export MAILU_VERSION="2.0.30"
export MAILU_PINNED_VERSION="2.0.30"
```

- Build and push the docker images

```console
docker buildx bake -f tests/build.hcl --push admin resolver
```

<p align="leftr"><img src="docs/assets/logomark.png" alt="Mailu" height="200px"></p>


Mailu is a simple yet full-featured mail server as a set of Docker images.
It is free software (both as in free beer and as in free speech), open to
suggestions and external contributions. The project aims at providing people
with an easily setup, easily maintained and full-featured mail server while
not shipping proprietary software nor unrelated features often found in
popular groupware.

Most of the documentation is available on our [Website](https://mailu.io),
you can also [try our demo server](https://mailu.io/master/demo.html)
before setting up your own, and come [talk to us on Matrix](https://matrix.to/#/#mailu:tedomum.net).

Features
========

Main features include:

- **Standard email server**, IMAP and IMAP+, SMTP and Submission with auto-configuration profiles for clients
- **Advanced email features**, aliases, domain aliases, custom routing, full-text search of email attachments
- **Web access**, multiple Webmails and administration interface
- **User features**, aliases, auto-reply, auto-forward, fetched accounts, managesieve
- **Admin features**, global admins, announcements, per-domain delegation, quotas
- **Security**, enforced TLS, DANE, MTA-STS, Letsencrypt!, outgoing DKIM, anti-virus scanner, [Snuffleupagus](https://github.com/jvoisin/snuffleupagus/), block malicious attachments
- **Antispam**, auto-learn, greylisting, DMARC and SPF, anti-spoofing
- **Freedom**, all FOSS components, no tracker included

![Domains](docs/assets/screenshots/domains.png)

Contributing
============

Mailu is free software, open to suggestions and contributions. All
components are free software and compatible with the MIT license. All
specific configuration files, Dockerfiles and code are placed under the
MIT license.
