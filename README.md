# tailscale-4via6

Minimal static web app for GitHub Pages that helps with:

- Converting IPv4 CIDR + site ID to a Tailscale 4via6 IPv6 route.
- Generating the corresponding MagicDNS host name format.

## Official docs

- Tailscale 4via6 subnet routers:
  - https://tailscale.com/docs/features/subnet-routers/4via6-subnets

## Useful notes

- 4via6 IPv6 format is:
  - `fd7a:115c:a1e0:b1a:0:SITE:YYYY:YYYY/P`
- `fd7a:115c:a1e0:b1a` is the fixed Tailscale prefix.
- The next block is always `0`.
- `SITE` is your site ID (this app accepts decimal or `0x` hex input, range `0..65535`).
- `YYYY:YYYY` is the IPv4 network address rendered as two 16-bit hex chunks.
- IPv6 prefix length conversion is:
  - $P = v4Prefix + 96$
  - Example: `/24 -> /120`
- Input CIDR is normalized to network address before conversion.
- MagicDNS host format from docs is:
  - `Q-R-S-T-via-X`
  - where `Q.R.S.T` is the IPv4 host and `X` is the site ID.
