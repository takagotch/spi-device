### spi-device
---
https://github.com/fivdi/spi-device

```
npm install spi-device
```

```js
const spi = require('spi-device');
const mcp3008 = spi.open(0, 0, (err) => {
  const message = [{
    sendBuffer: Buffer.from([0x01, 0xd0, 0x00]),
    receiveBuffer: Buffer.alloc(3),
    byteLength: 3,
    speedHz: 20000
  }];
  if(err) throw err;
  mcp3008.transfer(message, (err, message) => {
    if(err) throw err;
    const rawValue = ((message[0].receiveBuffer[1] & 0x03) << 8) +
      message[0].receiveBuffer[2];
    const voltage = rawValue * 3.3 / 1023;
    const celcius = (voltage - 0.5) * 100;
    console.log(celcius);
  });
});

```

```
```


