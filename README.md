# Proxy to Verdaccio for Unity Package Manager

## Installation

```bash
git clone git@github.com:monry/upm-proxy.git
cd upm-proxy/
cp .env.sample .env
vim .env
docker-compose up --build
```

## Setting

### `.env`

```.env
PORT=<port>
AUTH_TOKEN=<authorization-token>
REGISTRY_URL=<upm-registry-url>
```

| name | description |
| --- | --- |
| port | Port number to listen (default: 4873) |
| authorization-token | Authorization token obtained from registry server (Base64 format) |
| upm-registry-url | Registry URL |

### `Packages/manifest.json` in Unity Project

```js
{
  "scopedRegistries": [
    {
      "name": "Proxy Unity Package Manager Registry",
      "url": "http://localhost:4873",
      "scopes": [
        "dev.sample.upm"
      ]
    }
  ],
  "dependencies": {
    "dev.sample.upm.some-package": "1.0.0",
    // ...
  }
}
```

## Misc

You must set `url_prefix: http://localhost:4873` to Verdaccio configuration to replace all URL returning from Verdaccio API.
