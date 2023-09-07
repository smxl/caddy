# Caddy

Caddy2 with Addons cloudflare, trojan, naiveproxy, br, webdav

Caddy2 Lite with Addons cloudflare, trojan, naiveproxy

## Config Example

### cloudflare

```
{
    email PLACEHOLDER
}

    tls {
        dns cloudflare PLACEHOLDER
    }
```

### brotli

```
encode br zstd gzip
```

### webdav

```
order webdav before file_server

route /PATH/* {
    @notget {
        not method GET
    }
    route @notget {
        basicauth {
            USER PASSWORD
        }
        webdav {
          root /PATH
          prefix /PATH
        }
    }
    file_server browse
}
```

### trojan

```
order trojan before reverse_proxy

servers {
  listener_wrappers {
    trojan
  }
}
trojan {
  caddy
  no_proxy
  users PASSWORD
}

:443, https://DOMAIN {
	trojan {
		connect_method
		websocket
	}
}
```

### naive
```
:443, https://DOMAIN {
    route {
        forward_proxy {
            basic_auth USER PASSWORD
            hide_ip
            hide_via
            probe_resistance
        }
    }
}
```
