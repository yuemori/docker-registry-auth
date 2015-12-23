# Docker private registry
## setup

```
$ sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout server.key -out server.pem
$ mkdir ssl
$ mv server* ssl
```

## configuration

Configuration file is `config/auth_config.yml`.
See the example config files in [cesanta/docker_auth](https://github.com/cesanta/docker_auth#installation-and-examples)

## enable insecure-registry in client

If you run private registry except on localhost, set `--insecure-registry` option to profile and restart docker daemon.

These example, please replace `my-registry` to your private registry address.

### MacOSX

```
$ docker-machine ssh default "echo $'EXTRA_ARGS=\"--insecure-registry my-registry:5000\"' | sudo tee -a /var/lib/boot2docker/profile && sudo /etc/init.d/docker restart"
```

### Ubuntu (Unverified)

```
$ echo "export other_args=\"--insecure-registry my-registry:5000\" | sudo tee -a /etc/default/docker && sudo service docker restart
```

### CentOS (Unverified)

```
$ echo "export other_args=\"--insecure-registry my-registry:5000\" | sudo tee -a /etc/sysconfig/docker && sudo service docker restart
```
