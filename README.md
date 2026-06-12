# ESnet Keycloak Theme

Custom Keycloak login theme for ESnet, built on the [Packets Design System](https://github.com/esnet/packets-design-system) design system.

Figma: https://www.figma.com/design/Ojhz4WLfjNvuFIG1fB268H/SSO-Login

## Setup

These instructions are for development, and may differ slightly for delopyment.

1) Install the [Keycloak distribution](https://www.keycloak.org/guides).

2) Clone the repository's contents into `keycloak-X.Y.Z/themes/esnet`.

```sh
cd keycloak-X.Y.Z/themes
git clone https://github.com/echennau/esnet-keycloak-theme esnet
```

3) Start the development server with the following command:

```sh
cd ..
bin/kc.sh start-dev \
    --spi-theme-static-max-age=-1 \
    --spi-theme-cache-themes=false \
    --spi-theme-cache-templates=false
```

4) Create initial administrator user.

5) Enable the theme by logging in as admin and going to Realm Settings > Themes > Login theme > esnet

6) Log out to see the theme applied to the login page. Refresh the page after changes to apply effects.

## Development

This repository applies styling to the login pages.

### Keycloak Theming Crash Course

Keycloak themes use layered inheritance.
Each theme declares a `parent` and only the files it specifies, with everything else inherited from the parent.

Inheritance chain: `esnet` -> `keycloak.v2` -> `base`

- `base` — all FreeMarker `.ftl` HTML templates
- `keycloak.v2` — Keycloak's PatternFly v5 CSS; overrides some base templates
- `esnet` (this theme) — Overrides the login template and applies Packets styling

Read more about Keycloak theming [here](https://www.keycloak.org/ui-customization/themes).

### Future Directions
- **Review other login pages**: The following pages still have some styling applied, but may need manual adjustment if they are enabled:
  - `register.ftl` — user registration
  - `login-reset-password.ftl` — forgot password
  - `login-update-password.ftl` — force password change
  - `login-config-totp.ftl` — TOTP setup (QR code page)
  - `error.ftl` — generic Keycloak error page
  - `info.ftl` — informational messages (e.g. email sent)
