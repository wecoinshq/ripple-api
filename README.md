# Ripple API

[![Build Status][build-status-svg]][build-status-url]
[![Go Report Card][goreport-svg]][goreport-url]
[![Docs][docs-godoc-svg]][docs-godoc-url]
[![License][license-svg]][license-url]

Ripple API provides a HTTP-RPC based API for the [`rippled` server](https://github.com/ripple/rippled). It is more REST-like than the existing interfaces and should be eaiser to use for those with REST API experience, while remaining close enough to the [`rippled` server's API](https://xrpl.org/rippled-api.html) to ensure maintenance, support and documenation should be eaiser than if a larger change was introduced.

## Installation

Ripple API can run as a stand-alone server using `net/http` or `fasthttp`. It can also run on AWS Lambda behind an AWS API Gateway Proxy. This is set by setting the `HTTP_ENGINE` environment variable to one of `nethttp`, `fasthttp` or `awslambda`.

## AWS Lambda

1. Use the `aws-package.sh` script to create a zip file to upload to AWS Lambda.
1. Change "Runtime settings"  > "Handler" to `main` from `hello`

### Testing

Test with:

* `curl -XGET 'https://{gatewayId}.execute-api.{awsZone}.amazonaws.com/{stage}/api'`
* `curl -XPOST 'https://{gatewayId}.execute-api.{awsZone}.amazonaws.com/{stage}/api/v1/account_info' -H 'Content-Type: application/json' -d @docs/examples/endpoint_account_info_request.json`

## Heroku

Heroku relies on the `PORT` environment variable.

## API Spec

The API Spec is a work in progress and available at:

* [`spec_wecoins-ripple_openapi3.json`](spec_wecoins-ripple_openapi3.json)
* [`spec_wecoins-ripple_postman2.json`](spec_wecoins-ripple_postman2.json)

## Example Request

### API Request: HTTP API

```
POST /api/account_info

{
  "account": "rG1QQv2nh2gr7RCZ1P8YYcBUKCCN633jCn",
  "strict": true,
  "ledger_index": "current",
  "queue": true
}
```

```
curl -XPOST 'http://localhost:8080/api/account_info' -d '{"account": "rG1QQv2nh2gr7RCZ1P8YYcBUKCCN633jCn", "strict": true, "ledger_index": "current", "queue": true}'
```

### API Request: Websockets

```json
{
  "id": 2,
  "command": "account_info",
  "account": "r9cZA1mLK5R5Am25ArfXFmqgNwjZgnfk59",
  "strict": true,
  "ledger_index": "current",
  "queue": true
}
```

### API Request: JSON-RPC

```
POST /api/account_info

{
  "method": "account_info",
  "params": [
    {
      "account": "rG1QQv2nh2gr7RCZ1P8YYcBUKCCN633jCn",
      "strict": true,
      "ledger_index": "current",
      "queue": true
    }
  ]
}
```

 [build-status-svg]: https://github.com/wecoinshq/ripple-api/workflows/go%20build/badge.svg?branch=master
 [build-status-url]: https://github.com/wecoinshq/ripple-api/actions
 [goreport-svg]: https://goreportcard.com/badge/github.com/wecoinshq/ripple-api
 [goreport-url]: https://goreportcard.com/report/github.com/wecoinshq/ripple-api
 [docs-godoc-svg]: https://pkg.go.dev/badge/github.com/wecoinshq/ripple-api
 [docs-godoc-url]: https://pkg.go.dev/github.com/wecoinshq/ripple-api
 [license-svg]: https://img.shields.io/badge/license-MIT-blue.svg
 [license-url]: https://github.com/wecoinshq/ripple-api/blob/master/LICENSE