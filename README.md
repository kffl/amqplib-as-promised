## amqplib-as-promised

This module wrapping [amqplib node.js library](http://www.squaremobius.net/amqp.node/channel_api.html)
to provide classic `Promise` interface. (instead of original implementation using Bluebird promises)
Also, AMQP protocol closing channel when any error occurs. (even in case of using `checkQueue` method,
error is emitted and channel is closed, when queue does not exist) That library wrapper automatically
reconnects channel and returning error as a Promise `reject` response.


### Requirements

This module requires Node >= 8.

### Installation

```shell
npm install amqplib-as-promised
```

### Usage

(with `async` `await` syntax)

```js
const { Connection } = require('amqplib-as-promised')
const connection = new Connection(AMQP_URL)
await connection.init()
const channel = await connection.createChannel()
await channel.assertQueue(queueName)
await channel.sendToQueue(queueName, Buffer.from(testMessage))
await channel.close()
await connection.close()
```

typescript version

```ts
import { Connection } from 'amqplib-as-promised'
const connection = new Connection(AMQP_URL)
await connection.init()
const channel = await connection.createChannel()
await channel.assertQueue(queueName)
await channel.sendToQueue(queueName, Buffer.from(testMessage))
await channel.close()
await connection.close()
```

### API

#### Connection

| Method | arguments | return value | notes |
| --- | --- | --- | --- |
| *constructor* | **url**: string **options**?: amqplib.Options.Connect | Connection |  |
| init | - | Promise\<void\\> |  |
| createChannel | - | Promise\<Channel\> |  |
| close | - | Promise\<void\> |  |
| waitForClose | - | Promise\<void\> |  |


#### Channel

| Method | arguments | return value | notes |
| --- | --- | --- | --- |
| checkQueue | **queueName**: string | Promise\<amqplib.Replies.AssertQueue\> |  |
| assertQueue | **queueName**: string **options**?: amqplib.Options.AssertQueue | Promise\<amqplib.Replies.AssertQueue\> |  |
| deleteQueue | **queueName**: string **options**?: amqplib.Options.DeleteQueue | Promise\<amqplib.Replies.DeleteQueue\> |  |
| sendToQueue | **queueName**: string **content**: Buffer **options**?: amqplib.Options.Publish | Promise\<boolean\> |  |
| publish | **exchange**: string **queue**: string **content**: Buffer **options**?: amqplib.Options.Publish | Promise\<boolean\> |  |
| prefetch | **count**: number **global**: boolean | Promise\<void\> |  |
| consume | **queueName**: string **handler**: (message: amqplib.Message \| null) =\> any **options**?: amqplib.Options.Consume | Promise\<amqplib.Replies.Consume\> |  |
| cancel | **consumerTag**: string | Promise\<amqplib.Replies.Empty\> |  |
| get | **queueName**: string **options**?: amqplib.Options.Get | Promise\<Message \| false\> |  |
| ack | **message**: amqplib.Message **allUpTo**?: boolean | void |  |
| nack | **message**: amqplib.Message **allUpTo**?: boolean **requeue**?: boolean | void |  |
| close | - | Promise\<void\> |  |

### License

Copyright (c) 2017-2018 Tadeusz Wawszczak

[MIT](https://opensource.org/licenses/MIT)