# nova-novadb

Driver for NovaDB (Kyte's embedded B-tree engine) over its binary protocol. A Kyte package — fetch with:

```sh
kyte get https://github.com/kamlesh-nb/nova-novadb
```

```kyte
import novadb;
```

## Structure (SOLID)

Split by responsibility; consumers only touch the seam (`KyteDriver` / `KyteConnection`).

| Module       | Responsibility |
|--------------|----------------|
| `novadb`    | Seam: `KyteConnection impl Connection` + `KyteDriver impl Driver` + connect/startup. |
| `connection`     | Connection-string parsing (`ConnectionOptions`, `parse`). |
| `codec`   | Wire codec — frame builders + response decoders + `BtCursor`. |
| `typemap` | OID↔`DbType`, `DbValue`→SQL/bind text, `substituteParams`. |
| `proto`   | Async transport framing (`BtReader`, `BtFrame`, `readFrame`, `sendFrame`). |
