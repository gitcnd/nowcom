# nowcom (an espnow communications helper)

nowcom lets you easily send packed + compressed + encrypted data packets to one or all\* devices in range, and includes replay attack prevention

*. packed: you can send most python objects you want; e.g. `obj = [1, 2, 3.14159, {"hello":[b"from",toml.getenv('HOSTNAME')]}];n.send(obj)`
*. compressed: if you added `#define MICROPY_PY_DEFLATE_COMPRESS (1)` to your `mpconfigboard.h` when you build your micropython firmware, you can set `compress=True` and you data will be `defate.RAW` compressed (handy; max packet size is otherwise 234 bytes)
*. encrypted: using AES 256
*. integrity: packets are hashed with a secret salt to prevent junk-injection attacks
*. replay prevention: sequence-state system prevents data replay attacks and works without needing a time or clock

\* (yes - encrypted broadcasts work, unlike espnow native encryption)


## How to install

1. Grab the `nowcom.py` file (or if you are on MicroPython 1.24 the binary `nowcom.mpy` file)
2. the file to toye `/lib` or `/` folder on your esp32

## How to use

```python
import nowcom
n=nowcom.nowcom(debug=True,compress=False,key=b'!AES 16byte key!',salt=b'1~G:[7rhmalS')
obj = [1, 2, 3.14159, {"hello":[b"from",'HOSTNAME']}]
n.send(obj)        # set tgt=b'somepc' to send only to them
n.recv(wait=1001)  # set tgt=[b'somepc',b'anothr'] to listen only for messages from them
```

## Example

coming soon
