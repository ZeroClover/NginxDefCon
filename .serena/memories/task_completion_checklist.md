# Task Completion Checklist

- Run syntax validation: `nginx -t -c $(pwd)/nginx.conf` (or dockerized validation).
- If deploying to an existing host:
  - Backup current configs.
  - Copy `nginx.conf`, `conf.d/*`, and `snippets/*` into appropriate paths.
  - Verify included paths exist or update `include` directives to match your environment.
  - Reload Nginx and confirm no errors.
- Verify behavior:
  - HTTP/80 returns 444 except for `/.well-known` challenge paths.
  - TLS/443 rejects handshake by default (`ssl_reject_handshake on;`).
  - Security headers present when served from a proper vhost that includes `snippets/security.conf`.
  - Compression works if modules available.
  - HTTP/2 and HTTP/3 negotiate successfully if supported by build.
- Log review: Check `/var/log/nginx/error.log` for warnings.
- Document environment-specific overrides in site configs under `sites-enabled` or `conf.d`.
