# Tailscale Egg

[Tailscale](https://tailscale.com/) is a zero-config VPN that creates a secure mesh network (Tailnet) between your servers and devices. This Egg allows you to run Tailscale directly within a **Pelican** or **Pterodactyl** container using userspace networking.

## File Identification
Ensure you are using the correct file for your specific panel:
- **Pelican Panel:** `egg-tailscale.json`
- **Pterodactyl Panel:** `pterodactyl-egg-tailscale.json`

---

## Host Requirements
To use **Exit Node** or **Subnet Routing** features, you must enable IP forwarding on the underlying host system (the machine running Wings or Pelican-Bird).

### 1. Configure IP Forwarding
Add or modify the following lines in `/etc/sysctl.conf`:

```
net.ipv4.ip_forward=1
net.ipv6.conf.all.forwarding=1
```

*Note: If your system lacks /etc/sysctl.conf, create a file at /etc/sysctl.d/99-ipforward.conf instead.*

### 2. Apply Changes
Run the command corresponding to your change:
- For sysctl.conf: sudo sysctl -p
- For sysctl.d: sudo sysctl --system

---

## Configuration & Variables

| Variable | Env Variable | Description |
|----------|--------------|-------------|
| **Tailscale Auth Key** | TS_AUTHKEY | **Required.** Your auth key (starts with tskey-auth...). Generate one at https://login.tailscale.com/admin/settings/keys. |
| **Server Name** | SERVER_NAME | The hostname that will appear in your Tailscale machine list. |
| **Enable Exit Node** | ENABLE_EXIT_NODE | Set to true to allow other devices to route their internet traffic through this server. |
| **Subnet Routes** | TS_ROUTES | Comma-separated list (e.g., 192.168.1.0/24) to expose local networks. |

---

## Setup Instructions

1. **Generate a Key:** Go to the Tailscale Admin Console and generate a new Auth Key.
2. **Apply Variables:** Input the key and your desired settings into the Egg variables.
3. **Start the Server:** Launch the container.
4. **Admin Approval:** If you enabled Exit Nodes or Subnet Routes, you MUST manually approve them in the Tailscale Admin Console (https://login.tailscale.com/admin/machines) by clicking "Edit route settings" in the device menu.
