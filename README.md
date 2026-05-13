# amalgame-net-websocket

RFC 6455 **WebSocket client** for [Amalgame](https://github.com/amalgame-lang/Amalgame).
Text frames over plain TCP (`ws://`), in-process SHA-1 + Base64
for the handshake — **no OpenSSL dependency**.

Originally shipped in amc's bundled `runtime/Amalgame_WebSocket.h`;
extracted into this external package as part of the v0.7.8
bundled-runtime trim.

## Install

```bash
amc package add net-websocket                  # via the curated index
amc package add github.com/amalgame-lang/amalgame-net-websocket@v0.1.0
```

Requires **amc 0.7.7+**.

## Surface

```amalgame
import Amalgame.Net.WebSocket

class Program {
    public static void Main() {
        let ws: WebSocket = WebSocket.Connect("echo.websocket.org", 80, "/", "")
        if (ws.IsConnected()) {
            ws.SendText("hello")
            let reply: string = ws.RecvText()
            Console.WriteLine("got: " + reply)
            ws.Close()
        }
    }
}
```

## Scope (v0.1)

- ✅ `ws://` (plain TCP)
- ✅ Text frames (op 0x1)
- ✅ Sec-WebSocket-Accept handshake (in-process SHA-1 + Base64)
- ✅ Server-initiated `Close` frame is honored (`IsConnected()`
  flips to `false`)
- ❌ `wss://` (TLS) — deferred to v0.2
- ❌ Binary frames (op 0x2)
- ❌ Continuation frames (op 0x0)
- ❌ per-message-deflate extension
- ❌ HTTP subprotocols header

Deferred features land when a real consumer needs them.

## Tests

```bash
./tests/run_tests.sh /path/to/amc
```

In-process tests (handshake key against the RFC test vector,
error paths for refused-connection / DNS failure) run in CI.
A live-server smoke test is opt-in and out-of-band.

## License

Apache-2.0 — see `LICENSE`. No vendored third-party code; the
SHA-1 + Base64 implementations are small public-domain references
inlined in `runtime/Amalgame_WebSocket.h`.
