# nova-novadb

Driver for NovaDB (Nova's embedded B-tree engine) over its binary protocol. A Nova package — fetch with:

```sh
nova get https://github.com/kamlesh-nb/nova-novadb
```

```nova
import novadb;
```

## Structure (SOLID)

Split by responsibility; consumers only touch the seam (`NovaDriver` / `NovaConnection`).

| Module       | Responsibility |
|--------------|----------------|
| `novadb`    | Seam: `NovaConnection impl Connection` + `NovaDriver impl Driver` + connect/startup. |
| `connection`     | Connection-string parsing (`ConnectionOptions`, `parse`). |
| `codec`   | Wire codec — frame builders + response decoders + `BtCursor`. |
| `typemap` | OID↔`DbType`, `DbValue`→SQL/bind text, `substituteParams`. |
| `proto`   | Async transport framing (`BtReader`, `BtFrame`, `readFrame`, `sendFrame`). |
