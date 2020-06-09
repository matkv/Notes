# CentOS

To enable connections from the network (for example from the host to a VM running the server) we need to run this command:

```
`setsebool httpd_can_network_connect=1`
```

PHP errors can be enabled in `etc/php.ini`.