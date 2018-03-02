# Python sample oracle

## Introduction

This is a sample oracle written in Python giving basic functionality similar to the popular [Oraclize](http://www.oraclize.it/) service on the Ethereum blockchain.

The full source code is [here](https://github.com/aeternity/aepp-sdk-python/blob/master/examples/oracle_operator_example.py)

From the comments in the code:

```
   An oracle that can provide data from JSON APIs from the web.

    Just provide an URL that returns JSON for a GET request

    And provide the a jq-style query:
        (but it's reduced to alphanumeric non-quoted key traversal for plain
        objects and lists, e.g.)

        {'this': {'is': ['some', 'awesome'], 'api': 'result'}}}

        with the parameter
            jq='.this.is[1]'
        would return
            "awesome"
```

## Overview

In order to implement an oracle in Python, you must define a class which extends the Oracle class, and implements the method `get_response`, and connect to an Epoch instance which will host your oracle.

## Imports

```
from aeternity import Config
from aeternity import EpochClient
from aeternity import Oracle

```

## Connecting to Epoch and initializing

```

dev1_config = Config(local_port=3013, internal_port=3113, websocket_port=3114)
oraclef_jean = OraclefJean(
    # example spec (this spec is fictional and will be defined later)
    query_format='''{'url': 'str', 'jq': 'str'}''',
    # example spec (this spec is fictional and will be defined later)
    response_format='''{'status': 'error'|'ok', 'message': 'str', 'data': {}}''',
    default_ttl=50,
    default_query_fee=4,
    default_fee=6,
    default_query_ttl=10,
    default_response_ttl=10,
)
client = EpochClient(config=dev1_config)
client.register_oracle(oraclef_jean)
client.listen_until(oraclef_jean.is_ready)
```

In this example we use the default Epoch ports, and our oracle has a ttl of 50, a query fee of 4 and request/response ttls of 10. In a real oracle implementation the ttl would almost certainly be longer.

## Handling clients

```
    def get_response(self, message):
        payload_query = message['payload']['query']
        payload_query = json.loads(payload_query)
        try:
            url, jq = payload_query['url'], payload_query['jq']
        except (KeyError, AssertionError) as exc:
            print(exc)
          return self._error('malformed query')
        try:
            json_data = requests.get(url).json()
        except:
            return self._error('request/json error')
        try:
            ret_data = self._jq_traverse(jq, json_data)
        except (KeyError, AssertionError):
            return self._error('error traversing json/invalid jq')
        # make sure the result is not huge
        ret_data = json.dumps(ret_data)
        if len(ret_data) > 1024:
            return self._error('return data is too big (>1024 bytes)')
        return self._success(ret_data)
```

In principle this is all that is required to create an oracle.


