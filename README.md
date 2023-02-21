The Oreos Project
==================

An ironfish provider implementation and utilities in TypeScript.

**Features:**

- Ironfish rpc over socket, both Tcp and Tls are supported
- Fully **TypeScript** ready, with definition files and full TypeScript source

**Advanced:**

As shown above, only part of rpc methods are supported by Oreos rpc service component. Therefore, Oreos provides another
way to perform rpc request.

```typescript
import { RpcTcpClient, RpcTlsClient } from 'oreos';

const tcpClient = new RpcTcpClient(ip, port, rpcAuthToken);
const tlsClient = new RpcTlsClient(ip, port, rpcAuthToken);

// to perform getBalance
const getBalanceRequest: GetBalanceRequest = {
  account: 'default',
  confirmations: 2,
};
const response = await tlsClient.send("wallet/getBalance", getBalanceRequest);
```

Please refer to [HowToRpc.md](/docs/HowToRpc.md) for more details about rpc.
