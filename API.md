
## Python

### Chat example

#### Install and run

```
pip3 install websocket-client
python3 example_chat.py
```

Test the result with https://elektron.live/example_python

#### Code

```py
# example_chat.py

import websocket
import json
from datetime import datetime

channel = 'example_python'
ws_url = 'wss://ws-fggq5.ondigitalocean.app'

try:
    import thread
except ImportError:
    import _thread as thread


def on_message(ws, message):
    parsed_message = json.loads(message)
    if (parsed_message['channel'] == channel and parsed_message['type'] == 'CHAT'):
        print(parsed_message)


def on_open(ws):
    def run(*args):
        message = {
            'datetime': datetime.now().isoformat(),
            'channel': channel,
            'id': 'fizxvgdynclkojwq',
            'userId': 'davhtwsgmblecfon',
            'userName': 'Python user',
            'type': 'CHAT',
            'value': 'Hello from Python!'
        }
        ws.send(json.dumps(message))

    thread.start_new_thread(run, ())


if __name__ == "__main__":
    ws = websocket.WebSocketApp(ws_url,
                                on_message=on_message,
                                )
    ws.on_open = on_open
    ws.run_forever()
```

### Image example

```
import websocket
import json
from datetime import datetime
from urllib.request import urlopen

channel = 'example_python'
ws_url = 'wss://ws-fggq5.ondigitalocean.app'

try:
    import thread
except ImportError:
    import _thread as thread


def on_message(ws, message):
    parsed_message = json.loads(message)
    if (parsed_message['channel'] == channel and parsed_message['type'] == 'IMAGE'):
        with urlopen(parsed_message['value']) as response:
            with open(parsed_message['userId'] + '.jpg', 'wb') as f:
                f.write(response.read())


def on_open(ws):
    def run(*args):
        message = {
            'datetime': datetime.now().isoformat(),
            'channel': channel,
            'id': 'fizxvgdynclkojwq',
            'userId': 'davhtwsgmblecfon',
            'userName': 'Python user',
            'type': 'CHAT',
            'value': 'Hello from Python!'
        }
        ws.send(json.dumps(message))

    thread.start_new_thread(run, ())


if __name__ == "__main__":
    ws = websocket.WebSocketApp(ws_url,
                                on_message=on_message,
                                )
    ws.on_open = on_open
    ws.run_forever()
```
