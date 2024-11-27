# Nginx Role

An Ansible role to install and configure Nginx with customizable site configurations for serving static files and proxying requests.

## Requirements

Ensure that the target hosts meet the following requirements:
- The `apt` package manager is available on the target system.
- Template-specific variables are set, such as `static_files_path`, `proxy_pass_url`, and `worker_connections`.

## Role Variables

The following variables can be customized in `defaults/main.yml`:

| Variable               | Description                                       | Default Value                      |
|------------------------|---------------------------------------------------|------------------------------------|
| `nginx_conf_template`  | Path to the Jinja2 template for the main Nginx config | `nginx.conf.j2`                  |
| `nginx_site_template`  | Path to the Jinja2 template for the default site configuration | `default-site.conf.j2`           |
| `nginx_conf_dest`      | Path to the main Nginx configuration file        | `/etc/nginx/nginx.conf`           |
| `nginx_site_available` | Path to Nginx's available site configuration     | `/etc/nginx/sites-available/default` |
| `nginx_site_enabled`   | Path to Nginx's enabled site configuration       | `/etc/nginx/sites-enabled/default` |
| `worker_connections`   | The number of connections per worker process     | `1024`                            |

Additionally, you can set the following variables for the Nginx templates:
- `static_files_path`: Directory for static files to serve (e.g., `/var/www/static`).
- `proxy_pass_url`: Upstream server URL for proxying requests (e.g., `http://127.0.0.1:8080`).

## Dependencies

This role has no dependencies on other Galaxy roles.

## Example Playbook

Here is an example of how to use this role:

```yaml
- hosts: servers
  vars:
    static_files_path: "/var/www/static"
    proxy_pass_url: "http://127.0.0.1:8080"
    worker_connections: 1024
  roles:
    - role: nginx
