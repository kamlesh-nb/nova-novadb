# nova-novadb

Driver for NovaDB (Nova's embedded B-tree engine) over its binary protocol. A Nova package — fetch with:

```sh
nova get https://github.com/kamlesh-nb/nova-novadb
```

```nova
import btreedb;
```

## Structure (SOLID)

Split by responsibility; consumers only touch the seam (`BTreeDriver` / `BTreeConnection`).

| Module       | Responsibility |
|--------------|----------------|
| `btreedb`    | Seam: `BTreeConnection impl Connection` + `BTreeDriver impl Driver` + connect/startup. |
| `bt_dsn`     | Connection-string parsing (`BtDsn`, `parseDsn`). |
| `bt_codec`   | Wire codec — frame builders + response decoders + `BtCursor`. |
| `bt_typemap` | OID↔`DbType`, `DbValue`→SQL/bind text, `substituteParams`. |
| `bt_proto`   | Async transport framing (`BtReader`, `BtFrame`, `readFrame`, `sendFrame`). |
