# Project Overview

- Purpose: Provide a hardened, default Nginx configuration scaffold, including sensible security headers, compression, QUIC/HTTP3, OCSP, and safe defaults for 80/443 with a deny-all posture.
- Tech Stack: Nginx configuration files (`nginx.conf`, `conf.d/*.conf`, `snippets/*.conf`). No app code.
- Structure:
  - `nginx.conf`: global worker, events, stream, and http blocks; includes `conf.d`, `upstream.d`, `sites-enabled`.
  - `conf.d/default.conf`: default vhost for 80/443 (HTTP/2+3 enabled, deny all on TLS via `ssl_reject_handshake`, 444 on port 80), ACME/PKI paths allowed.
  - `conf.d/upgrade.conf`: `map` for `Upgrade`/`Connection` headers.
  - `snippets/security.conf`: security headers and dotfile protection.
  - `snippets/compress.conf`: gzip and brotli compression types and levels.
- Conventions: Keep defaults minimal, modular via `include` statements; avoid exposing content by default; use Cloudflare-friendly log format.
- Entry points: This repo ships configs only; deploy by copying files into an Nginx-compatible filesystem layout or mounting into a container image.
