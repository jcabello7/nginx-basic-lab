# nginx-basic-lab

The lightweight, card-style NGINX test page used by `nginx_test2` through
`nginx_test5` before the PHP HTTP Lab inspector was introduced on `nginx_test1`.

The page identifies its backend, shows the actual NGINX server port for each
request, and displays the browser's current path. The configurations use only
NGINX and inline HTML/CSS/JavaScript; no PHP application or external assets are
required for this basic page.

## Templates

- `templates/site-80-443.conf`: backends listening on HTTP 80 and HTTPS/QUIC 443
  (`nginx_test2`, `nginx_test3`).
- `templates/site-80-443-8443.conf`: backends listening on HTTP 80, HTTPS 443,
  and HTTPS/QUIC 8443 (`nginx_test4`, `nginx_test5`).

Before using a template, set its `$backend_name` to the intended container name
and ensure `/config/nginx/ssl.conf` contains the container's existing certificate
configuration. Copy it to `/config/nginx/site-confs/default.conf`, run
`nginx -t`, and reload NGINX. Keep a copy of the active configuration first.

These templates preserve the test listener layout and the existing LinuxServer
certificate include. They do not manage Unraid Docker templates, DNS, NAT, firewall
rules, or Cloudflare configuration.

## Example page behavior

`nginx_test4` requested over port 8443 at `/diagnostics/ping` displays:

```text
nginx_test4 backend on port 8443
Path: /diagnostics/ping
```
