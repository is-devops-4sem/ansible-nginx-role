# Nginx Role

An Ansible role to install and configure Nginx with customizable site configurations.

## Requirements

Ensure that the target hosts meet the following requirements:
- The `apt` package manager is available on the target system.
- Template-specific variables are set, such as `static_files_path` and `proxy_pass_url`.

## Role Variables

The following variables can be customized in `defaults/main.yml`:

| Variable              | Description                                   | Default Value               |
|-----------------------|-----------------------------------------------|-----------------------------|
| `nginx_site_template` | Path to the Jinja2 template for Nginx config | `nginx.conf.j2`            |
| `nginx_site_available`| Path to Nginx's available site configuration | `/etc/nginx/sites-available/default` |
| `nginx_site_enabled`  | Path to Nginx's enabled site configuration   | `/etc/nginx/sites-enabled/default` |

Additionally, you can set the following variables for the Nginx template:
- `static_files_path`: Directory for static files to serve.
- `proxy_pass_url`: Upstream server URL for proxying requests.

## Dependencies

This role has no dependencies on other Galaxy roles.

## Example Playbook

Here is an example of how to use this role:

```yaml
- hosts: servers
  vars:
    static_files_path: "/var/www/static"
    proxy_pass_url: "http://localhost:8000"
  roles:
    - role: nginx
```
