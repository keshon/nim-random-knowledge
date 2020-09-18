[taken from here](https://github.com/yglukhov/nim-jwt/issues/11#issuecomment-694504078)

...just need to uncomment this in jwt.nim
```nim
  # of ES256:
  #   result = crypto.bearVerifyECPem(data, secret, signature, addr sha256Vtable, addr ecPrimeI15, sha256SIZE)
```
it fails with jwt.nim, and works with benmcollins/libjwt

```nim
#[
from https://jwt.io/ ES256
]#
import pkg/jwt
import tables, json

proc test1() =
  let pub = """
-----BEGIN PUBLIC KEY-----
MFkwEwYHKoZIzj0CAQYIKoZIzj0DAQcDQgAEEVs/o5+uQbTjL3chynL4wXgUg2R9
q9UU8I5mEovUf86QZ7kOBIjJwqnzD1omageEHWwHdBO6B+dFabmdT9POxg==
-----END PUBLIC KEY-----
"""
  let priv = """
-----BEGIN PRIVATE KEY-----
MIGHAgEAMBMGByqGSM49AgEGCCqGSM49AwEHBG0wawIBAQQgevZzL1gdAFr88hb2
OF/2NxApJCzGCEDdfSp6VQO30hyhRANCAAQRWz+jn65BtOMvdyHKcvjBeBSDZH2r
1RTwjmYSi9R/zpBnuQ4EiMnCqfMPWiZqB4QdbAd0E7oH50VpuZ1P087G
-----END PRIVATE KEY-----
"""
  let token = "eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWUsImlhdCI6MTUxNjIzOTAyMn0.tyh-VfuzIxCyGYDlkBA7DfyjrqmSHu6pQ2hoZuFqUSLPNY2N0mpHb3nk5K17HWP_3cYHBw7AhHale5wky6-sVA"
  let jwt = token.toJWT()
  let ok = verify(jwt, pub , alg = SignatureAlgorithm.ES256)
  doAssert ok # fails

test1()
```
