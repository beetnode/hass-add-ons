# izBoard Add-on

**izBoard** displays your Home Assistant dashboards on battery-powered E-Paper devices. Your device automatically fetches updated dashboard images from this add-on on a schedule you control. The add-on converts your Home Assistant dashboards into the right format for E-Paper displays. Because the device only uses power during updates, a single battery charge can last weeks or even months.

**Project Repository**: [izBoard](https://github.com/izdev-digital/e-paper-dashboard)

The add-on image (`izdevdigital/izboard-addon`) is built and published by the izBoard project repository.

## Configuration

Set `CLIENT_URL` to the LAN URL that your E-Paper displays can reach. The default is
`http://homeassistant.local:8129`. Change the host or port if your network does not resolve
`homeassistant.local`, the add-on port is remapped, or the displays use a separate VLAN.

Do not use the Home Assistant ingress or cloud URL: those routes require a browser session and
are not reachable by the displays. Allow the display network to reach this URL through your
firewall.

## Data sources

Open **Connections** in izBoard to add Home Assistant and Google Calendar / Tasks accounts.
Connections are shared by everyone using the add-on.

- **Widget data**: the add-on's own Home Assistant instance is available automatically as
  **Dashboard Home Assistant** in the source picker; no token is needed.
- **Home Assistant dashboard screenshots**: these need a named Home Assistant connection with a
  long-lived access token (paste one from your Home Assistant profile, or use **Sign in**). The
  add-on cannot create this token itself. The connection's server URL must be reachable from both
  your browser and the add-on; `homeassistant.local` often does not resolve inside add-on
  containers, so prefer the IP address.
- **Google Calendar / Tasks**: requires your own Google OAuth client and Home Assistant opened over
  HTTPS. The redirect URI shown on the Connections page includes the ingress path; update it in
  Google Cloud if you reinstall the add-on. See the
  [provider setup guide](https://github.com/izdev-digital/e-paper-dashboard/blob/master/software/docs/data-provider-plugins.md).

## Support

For issues, feature requests, or questions:
- [Report an issue](https://github.com/izdev-digital/hass-add-ons/issues)
- [View add-on repository](https://github.com/izdev-digital/hass-add-ons)
- [View izBoard project](https://github.com/izdev-digital/e-paper-dashboard)

## Supported Architectures

Currently supported architectures:
- `amd64`
- `arm64`

**Note**: Home Assistant dashboard screenshots use an optional rendering component (Playwright and
Chromium). It is downloaded from the izBoard GitHub releases on first use, so the add-on needs
internet access, and it requires sufficient RAM and CPU; it may not run reliably on low-powered
devices. Custom layout dashboards do not need it.
