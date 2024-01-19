# Manual Testing for Email Enumeration Protection

Using a real Firebase project, manual testing of endpoints and their responses with Email Enumeration Protection enabled/disabled

----
## createUserWithEmailAndPassword (no difference)
### User Exists
#### Enabled
```json
{
  "error": {
    "code": 400,
    "message": "EMAIL_EXISTS",
    "errors": [
      {
        "message": "EMAIL_EXISTS",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```
#### Disabled
```json
{
  "error": {
    "code": 400,
    "message": "EMAIL_EXISTS",
    "errors": [
      {
        "message": "EMAIL_EXISTS",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```
----
## signInWithEmailAndPassword
### No User
#### Enabled
```json
{
  "error": {
    "code": 400,
    "message": "INVALID_LOGIN_CREDENTIALS",
    "errors": [
      {
        "message": "INVALID_LOGIN_CREDENTIALS",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```
#### Disabled
```json
{
  "error": {
    "code": 400,
    "message": "EMAIL_NOT_FOUND",
    "errors": [
      {
        "message": "EMAIL_NOT_FOUND",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```

### Wrong password
#### Enabled
```json
{
  "error": {
    "code": 400,
    "message": "INVALID_LOGIN_CREDENTIALS",
    "errors": [
      {
        "message": "INVALID_LOGIN_CREDENTIALS",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```
#### Disabled
```json
{
  "error": {
    "code": 400,
    "message": "INVALID_PASSWORD",
    "errors": [
      {
        "message": "INVALID_PASSWORD",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```

### User Disabled
#### Enabled
```json
{
  "error": {
    "code": 400,
    "message": "USER_DISABLED",
    "errors": [
      {
        "message": "USER_DISABLED",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```

#### Disabled
```json
{
  "error": {
    "code": 400,
    "message": "USER_DISABLED",
    "errors": [
      {
        "message": "USER_DISABLED",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```

### User Disabled + wrong Password
#### Enabled
```json
{
  "error": {
    "code": 400,
    "message": "USER_DISABLED",
    "errors": [
      {
        "message": "USER_DISABLED",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```

#### Disabled
```json
{
  "error": {
    "code": 400,
    "message": "USER_DISABLED",
    "errors": [
      {
        "message": "USER_DISABLED",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```
----
## fetchSignInMethodsForEmail
### No User
#### Enabled
```json
{
  "kind": "identitytoolkit#CreateAuthUriResponse",
  "sessionId": "ehpfdpyNv2J0jH3bOmw2auF4PrM"
}
```

#### Disabled
```json
{
  "kind": "identitytoolkit#CreateAuthUriResponse",
  "registered": false,
  "sessionId": "OqMNF-1Tp8s-pUJhkuvIMVy4_6A"
}
```

### User exists
#### Enabled
```json
{
  "kind": "identitytoolkit#CreateAuthUriResponse",
  "sessionId": "yDuvwZcbeauTSZPScXCkcTCNvWk"
}
```

#### Disabled
```json
{
  "kind": "identitytoolkit#CreateAuthUriResponse",
  "allProviders": [
    "password"
  ],
  "registered": true,
  "sessionId": "5jcQNCwU4T7cA_VAocfrHaSWNME",
  "signinMethods": [
    "password"
  ]
}
```

### User Disabled
#### Enabled
```json
{
  "kind": "identitytoolkit#CreateAuthUriResponse",
  "sessionId": "ZqNinTT2DiVEMxJdc_sgJv617Sw"
}
```
#### Disabled
```json
{
  "kind": "identitytoolkit#CreateAuthUriResponse",
  "allProviders": [
    "password"
  ],
  "registered": true,
  "sessionId": "fT9UUkEhOqQ4d-MJ5me6RulFX9E",
  "signinMethods": [
    "password"
  ]
}
```
----
## sendPasswordResetEmail
### No User
#### Enabled
```json
{
  "error": {
    "code": 400,
    "message": "EMAIL_NOT_FOUND",
    "errors": [
      {
        "message": "EMAIL_NOT_FOUND",
        "domain": "global",
        "reason": "invalid"
      }
    ]
  }
}
```
#### Disabled
```json
{
  "kind": "identitytoolkit#GetOobConfirmationCodeResponse",
  "email": "fake@fake.fake"
}
```
### User exists
#### Enabled
```json
{
  "kind": "identitytoolkit#GetOobConfirmationCodeResponse",
  "email": "fake@fake.fake"
}
```
#### Disabled
```json
{
  "kind": "identitytoolkit#GetOobConfirmationCodeResponse",
  "email": "fake@fake.fake"
}
```
### User Disabled
#### Enabled
```json
{
  "kind": "identitytoolkit#GetOobConfirmationCodeResponse",
  "email": "fake@fake.fake"
}
```
#### Disabled
```json
{
  "kind": "identitytoolkit#GetOobConfirmationCodeResponse",
  "email": "fake@fake.fake"
}
```