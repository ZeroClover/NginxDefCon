# Repository Guidelines

## Project Structure & Module Organization
- `nginx.conf`: Global worker, events, stream, and http config. Includes `conf.d/*.conf`, `upstream.d/*.conf`, and `sites-enabled/*`.
- `conf.d/`: Global and default server configs (e.g., `default.conf`, `upgrade.conf`).
- `snippets/`: Reusable includes (e.g., `security.conf`, `compress.conf`). Reference these from site configs as needed.
- External paths like `/etc/nginx/sites-enabled` and `/etc/nginx/upstream.d` are expected in deployment environments.

## Build, Test, and Development Commands
- Validate syntax: `nginx -t -c $(pwd)/nginx.conf`
- Docker validation (no local install): `docker run --rm -v $(pwd):/etc/nginx:ro nginx:alpine nginx -t`
- Run locally (advanced): `sudo nginx -c $(pwd)/nginx.conf` then `nginx -s reload`
- Quick checks:
  - HTTP: `curl -vI http://localhost` (expect 444 except `/.well-known/*`)
  - TLS/HTTP2: `curl -vkI https://localhost --http2`
  - HTTP/3 (if supported): `curl -vkI https://localhost --http3-only`

## Coding Style & Naming Conventions
- Indentation: 4 spaces; one directive per line; braces on same line as blocks.
- Directives: lower-case; use descriptive filenames with `.conf` (e.g., `rate-limit.conf`).
- Modularity: keep `nginx.conf` minimal; add features via `conf.d/*.conf` and `snippets/*.conf`.
- Security-first defaults: deny by default; only allow `/.well-known` challenge paths; do not serve content from the default server.

## Testing Guidelines
- Always run `nginx -t` before commits/PRs.
- Validate behavior with `curl` for ports 80/443. Confirm: 80 returns 444 (except challenges); 443 may reject handshake by default until a proper vhost is configured.
- If enabling HTTP/3 or brotli, ensure your build supports them; otherwise gate changes behind optional includes.

## Commit & Pull Request Guidelines
- Commit style: Conventional Commits (e.g., `feat(conf): enable brotli`, `fix(security): tighten CSP`, `chore: rename snippet`).
- PRs should include:
  - What changed and why, with sample directives/snippet usage.
  - How you validated (`nginx -t`, docker command, and `curl` results).
  - Any impact to defaults, and docs updates (README/snippets) if applicable.

## Security & Configuration Tips
- Keep `ssl_reject_handshake on;` in the default TLS server; add real vhosts in `sites-enabled/*`.
- Prefer `snippets/security.conf` and `snippets/compress.conf` in site configs rather than globally if compatibility is uncertain.
