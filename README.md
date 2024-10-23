# NodeCat
A port of Akamais Edgeworker CAT implementation (https://github.com/akamai/edgeworkers-examples/tree/master/delivery/media/cat) to NodeJS.

Not all claims are supported.


# NodeCat Service

Provides a backend with endpoint to create and verify common access tokens.

## Docker

```
docker build -t node-cat .
docker run -p 3000:3000 node-cat
```

## Usage

Generate token:

```
% curl 'http://localhost:3000/generateToken' \
  -H 'Content-Type: application/json' \
  --data-raw '{"exp":1829693926,"sub":"TheCatHunter","catr":{"expext":70,"renewabletype":2,"deadline":0}}'

  2D3RhEOhAQWhBFBha2FtYWlfa2V5X2hzMjU2WCqlBBptDunmAmxUaGVDYXRIdW50ZXIZARaiAAIBGEYGGmcZWXoFGmcZWXpYIDWdOGh_yV1OZx6eGrJ7RyjcXZM4FhDS9DGXyHMl_toU
```

Validate Token:

```
% curl -X POST http://localhost:3000/validateToken \
-H "Content-Type: application/json" \
-d '{"token": "2D3RhEOhAQWhBFBha2FtYWlfa2V5X2hzMjU2WCqlBBptDunmAmxUaGVDYXRIdW50ZXIZARaiAAIBGEYGGmcZWXoFGmcZWXpYIDWdOGh_yV1OZx6eGrJ7RyjcXZM4FhDS9DGXyHMl_toU"}'

{"status":"Token is valid","payload":{"exp":1829693926,"sub":"TheCatHunter","catr":{"renewal_type":2,"exp_extension":70},"iat":1729714554,"nbf":1729714554}}
```

## Generate keys

To use the code, please make sure to generate your own keys and insert them into the code.

```
node src/tokenManager.js

HS256 Key: feb0fd6be2dd86279a38f415dd85dbab56c97e3ff589ec7bb04e09c3fd98cb20
ES256 Private Key (PEM): -----BEGIN PRIVATE KEY-----
MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgZ6lvYoS0124WXH9F
LVMvCpglnrTOSNcycUDRIsxtKrihRANCAASbmVJ/LMW+BHkWoX4/ZdLxIAwDfb0d
P+XKDFozQHpJoo+9aIsWzjjyr/p5zPP6VBJwrz6nzql5IB8VSITnHayA
-----END PRIVATE KEY-----

ES256 Public Key (PEM): -----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEm5lSfyzFvgR5FqF+P2XS8SAMA329
HT/lygxaM0B6SaKPvWiLFs448q/6eczz+lQScK8+p86peSAfFUiE5x2sgA==
-----END PUBLIC KEY-----
```

