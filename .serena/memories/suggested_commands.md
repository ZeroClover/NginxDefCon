# Suggested Commands

- Validate config: `nginx -t -c $(pwd)/nginx.conf`
- Start Nginx (local custom path): `nginx -c $(pwd)/nginx.conf`
- Reload after changes: `nginx -s reload`
- Test TLS port locally: `curl -vkI https://localhost --http2` and `curl -vkI https://localhost --http3-only`
- Test HTTP port: `curl -vI http://localhost`
- Lint configs (dockerized): `docker run --rm -v $(pwd):/etc/nginx:ro nginx:alpine nginx -t`
- Inspect includes: `rg -n "include .*\.conf"`
- Check headers: `curl -sI https://example.com | sort` (run against deployed server)

Notes: HTTP/3 requires a build with QUIC/HTTP3; brotli requires the module. Adjust config if your nginx build lacks these modules.