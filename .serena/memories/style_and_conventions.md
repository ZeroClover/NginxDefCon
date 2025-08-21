# Style and Conventions

- File Layout: Organize reusable directives into `snippets/*.conf`; per-site or global maps in `conf.d/*.conf`.
- Includes: Prefer `include` for optional features; keep base `nginx.conf` clean.
- Security Defaults: Deny by default, allow only `/.well-known` challenge paths on port 80; TLS listener rejects handshake by default.
- Protocols: HTTP/2 and HTTP/3 enabled on 443; QUIC options enabled globally.
- Headers: Use `snippets/security.conf` for common security headers; apply `always` where appropriate.
- Compression: Use `snippets/compress.conf` and enable gzip/brotli with sane types.
- Logging: Minimal access logging by default; error log at `warn` level using Cloudflare-oriented format when enabled.
- Compatibility: Assumes modern Nginx with HTTP/3 and brotli modules available; adjust if not present.
