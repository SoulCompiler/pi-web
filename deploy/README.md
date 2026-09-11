# Local startup

This checkout uses port **16666**, with the production service listening at
http://127.0.0.1:16666 under the WSL user `soulcompiler`.

`pi-web.service` is installed at `~/.config/systemd/user/pi-web.service` and
enabled for the user manager. User lingering is enabled so the user manager
starts when Ubuntu-24.04 boots.

No Windows login startup item or WSL keepalive process is configured.
Pi Web starts when Ubuntu-24.04 starts and stops when the distribution stops.
The service does not open a browser.

Manage the service inside WSL:

```bash
systemctl --user status pi-web.service
systemctl --user restart pi-web.service
systemctl --user stop pi-web.service
journalctl --user -u pi-web.service -n 50 --no-pager
```

After source changes, stop the service, run `npm run build` in this checkout,
then start the service again. Port-only changes to the launcher do not require
rebuilding the Next.js output.

To disable automatic service startup, run
`systemctl --user disable --now pi-web.service`.
User lingering may serve other enabled services too; manage it separately.
