# Munin LiteSpeed Plugins for cPanel

A collection of robust Munin plugins designed to monitor LiteSpeed Web Server. These scripts have been specifically tested and adapted for cPanel environments and are written in modern, strict Perl for reliability.

Inspired by various community plugins and completely rewritten for robustness and cPanel compatibility.

# Plugins Included

This repository contains the following plugins:

- `litespeed_connections`: Monitors active and idle plain connections.
- `litespeed_ssl_connections`: Monitors active SSL connections.
- `litespeed_requests`: Monitors requests per second and in-process requests.
- `litespeed_throughtput`: Monitors network throughput (inbound/outbound) including SSL traffic.
- `litespeed_cache`: Monitors public, private, and static cache hit rates.
- `litespeed_extapp`: Monitors the external app backend (LSPHP), including in-use, idle, and waiting connections.
- `litespeed_hits`: An alternative script for monitoring cache hits.
- `litespeed_requests_post`: Monitors POST requests by parsing access logs.

# Installation (cPanel)

The installation process for cPanel involves placing the scripts in the cPanel-managed directory and then creating symbolic links to activate them.

```bash
# 1. Clone the repository to a temporary location
cd /root
git clone [https://github.com/kaellego/munin-litespeed-cpanel.git] munin-litespeed-cpanel

# 2. Move the plugin files to the cPanel munin directory
sudo mv munin-litespeed-cpanel/litespeed_* /usr/local/cpanel/3rdparty/share/munin/plugins/

# 3. Make the plugins executable
sudo chmod 755 /usr/local/cpanel/3rdparty/share/munin/plugins/litespeed_*

# 4. Create the symbolic links to activate the plugins
for plugin in /usr/local/cpanel/3rdparty/share/munin/plugins/litespeed_*; do
  sudo ln -sf "$plugin" "/etc/munin/plugins/$(basename "$plugin")"
done

# 5. Clean up the temporary directory
rm -rf munin-litespeed-cpanel

# 6. Restart the munin-node service
sudo systemctl restart munin-node
