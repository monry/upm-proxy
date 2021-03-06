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
HOSTNAME=<hostname>
AUTH_TOKEN=<authorization-token>
REGISTRY_URL=<upm-registry-url>
```

| name | description |
| --- | --- |
| HOSTNAME | Hostname to act as proxy (ex: `my-registry.local`) |
| AUTH_TOKEN | Authorization token obtained from registry server (Base64 format) |
| REGISTRY_URL | Registry URL to proxy |

### Generate Self-Signed Cerfiticates

Generate certificate and key file.
Simply to use [`mkcert`](https://github.com/FiloSottile/mkcert), if you use macOS or Linux.

```bash
mkcert -install
mkcert <hostname>
```

Put generated files into `nginx/` directory.

### `Packages/manifest.json` in Unity Project

```js
{
  "scopedRegistries": [
    {
      "name": "Proxy Unity Package Manager Registry",
      "url": "https://${hostname}",
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
