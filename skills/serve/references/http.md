# ingitdb serve --http

Start the HTTP REST API server. Exposes CRUD endpoints over HTTP.

## Command

```bash
ingitdb serve --http [--addr <host:port>] [--path <dir>]
```

## When to use

- Web app, mobile app, or service that needs to read or modify records over the network.
- Local development backend for a frontend.

## Notes

- Default bind address is platform-defined; pass `--addr` to override.
- Pair with reverse-proxy TLS for production.
