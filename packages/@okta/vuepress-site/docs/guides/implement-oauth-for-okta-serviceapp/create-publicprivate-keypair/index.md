---
title: Create a public/private key pair
---

The `private_key_jwt` client authentication method is the only supported method for OAuth service apps that want to get access tokens with Okta scopes.

The private key that you use to sign the JWT must have the corresponding public key registered in the [JWKSet](/docs/reference/api/oauth-clients/#json-web-key-set) of the OAuth service app. We recommend generating the public/private key pair first before creating the OAuth service app.

1. Run a version of the following OpenSSL command to generate a JWKS public/private key pair for testing. Okta supports both RSA and Elliptical Curve (EC) keys. In this example, we are generating an RSA key pair in Privacy Enhanced Mail (PEM) format with the following values:

    * Key size &mdash; 2048
    * Key use &mdash; signature
    * Algorithm &mdash; RSA256

2. Copy the Public Key from the `test-rsa-public.pem` file that you just generated.

> **Note:** Some Okta SDKs require that keys be in Privacy Enhanced Mail (PEM) format. If you are working with an Okta SDK that requires that the key be in PEM format, after you have generated the key pair, copy the public/private key pair into a [JWK to PEM Convertor tool](https://8gwifi.org/jwkconvertfunctions.jsp) and copy the private key to use when signing the JWT.

The JWKS should look something like this:

```json
{
  "keys": [
    {
      "kty": "RSA",
      "e": "AQAB",
      "use": "sig",
      "kid": "my_key_id",
      "alg": "RS256",
      "n": "u0VYW2-76A_lYg5NQihhcPJYYU9-NHbNaO6LFERWnOUbU7l3MJdmCailwSzjO76O-2GdLE-Hn2kx04jWCCPofnQ8xNmFScNo8UQ1dKVq0UkFK-sl-Z0Uu19GiZa2fxSWwg_1g2t-ZpNtKCI279xGBi_hTnupqciUonWe6CIvTv0FfX0LiMqQqjARxPS-6fdBZq8WN9qLGDwpjHK81CoYuzASOezVFYDDyXYzV0X3X_kFVt2sqL5DVN684bEbTsWl91vV-bGmswrlQ0UVUq6t78VdgMrj0RZBD-lFNJcY7CwyugpgLbnm4HEJmCOWJOdjVLj3hFxVVblNJQQ1Z15UXw"
    }
  ]
}
```

<NextSectionLink/>