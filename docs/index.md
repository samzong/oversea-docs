# Welcome to Oversea

- 采用了新的文档中心 [mkdocs.org](https://www.mkdocs.org).
- 使用的主题是 [mkdocs-material](https://squidfunk.github.io/mkdocs-material/)

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


<!-- hidden ? -->

```py
import requests
import json
import pandas as pd

url = "https://url/apiauth/v1/taobao/call_api"

headers = {
    'Content-Type': 'application/json',
    'Cookie': 'sessid=92d1af5a-bcb6-49c1-8147-f02941c30614'
    }


def main(store_id, api_url, method, params=None):
    payload = {
        "shop_id": store_id,
        "url": api_url,
        "method_type": method,
        "app_type": "ERP",
        }

    if params:
        payload['params'] = params

    response = requests.request(
        "POST", url, headers=headers, data=json.dumps(payload), timeout=10)

    return json.loads(response.json()['data'])['response']
```