# Caddy

Caddy2 with Addons trojan, naiveproxy

```
xcaddy build latest \
  --with github.com/imgk/caddy-trojan \
  --with github.com/caddyserver/forwardproxy@caddy2=github.com/klzgrad/forwardproxy@naive
  ...
```

## Config Example

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

#### naive client

https://github.com/klzgrad/naiveproxy/releases/latest

