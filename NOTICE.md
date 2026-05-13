# NOTICE — amalgame-net-websocket

## Authorship

Copyright 2026 Bastien Mouget. The Amalgame binding code in this
repository is original work — see `runtime/Amalgame_WebSocket.h`
and the `amalgame.toml` manifest.

This package is part of the Amalgame ecosystem
([github.com/amalgame-lang/Amalgame](https://github.com/amalgame-lang/Amalgame)).
It was extracted from amc's bundled `runtime/Amalgame_WebSocket.h`
during the v0.7.8 bundled-runtime trim.

## License

Licensed under the Apache License, Version 2.0 — see `LICENSE`.

## Third-party content

None. The SHA-1 + Base64 implementations needed for the
WebSocket handshake are vendored in-file (in
`runtime/Amalgame_WebSocket.h`) as small, public-domain
references (no OpenSSL or other crypto library required).
Frames are exchanged over raw POSIX sockets (`<sys/socket.h>`
on POSIX, `winsock2.h` on Windows via amc's runtime).
