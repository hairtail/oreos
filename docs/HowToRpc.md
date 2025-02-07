# Getting Started Rpc Service

**Methods supported by rpcService:**

- getBalance
- getTransaction
- getBlock
- getBlockInfo
- getChainInfo
- getStatus
- sendTransaction

**Perform rpc request with rpcService:**

```typescript
import { RpcService, RpcTcpClient, RpcTlsClient } from 'oreos';

const rpcProvider = new RpcService(ip, port, rpcAuthToken, 'TCP');
```

##### getBalance

```typescript
type GetBalanceRequest = {
  account?: string;
  assetId?: string;
  confirmations?: number;
};
type GetBalanceResponse = {
  account: string
  balances: {
    assetId: string
    confirmed: string
    unconfirmed: string
    unconfirmedCount: number
    blockHash: string | null
    sequence: number | null
  }[]
};

const getBalanceRequest: GetBalanceRequest = {
  account: 'default',
  confirmations: 2,
};

const response: GetBalanceResponse = await rpcProvider.getBalance(getBalanceRequest);
```

##### sendTransaction

```typescript
type SendTransactionRequest = {
  fromAccountName: string;
  receives: {
    publicAddress: string;
    amount: string;
    memo: string;
    assetId?: string;
  }[];
  fee: string;
  expiration?: number | null;
  expirationDelta?: number | null;
};
type SendTransactionResponse = {
  receives: {
    publicAddress: string;
    amount: string;
    memo: string;
    assetId?: string;
  }[];
  fromAccountName: string;
  hash: string;
};

const sendTransactionRequest: SendTransactionRequest = {
  fromAccountName: 'default',
  receives: [{
    publicAddress: '0xxxx0',
    amount: '100000',
    memo: 'send native oreo token',
  }],
  fee: '100',
};

const response = await rpcProvider.sendTransaction(sendTransactionRequest);
```

**Perform rpc request with rpcClient:**

Performing a customized rpc request that has not been supported by rpcService with `rpcTcpClient` and `rpcTlsClient`.

##### createAccount

```typescript
import { RpcTcpClient, RpcTlsClient } from 'oreos';

const tlsClient = new RpcTlsClient(ip, port, rpcAuthToken);

const createAccountRequest = {
  name: 'hello',
  default: true
};

const response = await tlsClient.send("wallet/create", createAccountRequest);
```

Refer to [rpc](https://github.com/iron-fish/ironfish/tree/master/ironfish/src/rpc/routes) for request and response
interface.
