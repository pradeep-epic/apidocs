## This documentation describes the flow of APIs listed at 
[Postman Documentation](https://documenter.getpostman.com/view/8770428/SWTEavk7)

### Initial sign in and check

Sign In

``` POST /api/v1/users/sign_in```

To call this the client will need a client id and client secret. Please
contact Engineering to obtain the same.
The response will provide an access_token and a refresh_token. All subsequent
requests will need to use access_token as the user_access_token parameter

Verify Sign in

``` GET /api/v1/users/me?access_token={{user_access_token}} ```

To verify your credentials and to ensure that everything is working fine.

### Earn APIs
There is only one Earn API that the client has to implement for real time points
earn.

``` POST /api/v1/evaluations/earn?access_token={{user_access_token}}```

The body of this request specifies what is needed for the earn operation. These
parameters have to be the same parameters that are configured in any program for
this client. Please refer to the LMS Dashboard for program creation.

There is also a bulk earn API that is essentially the same API as above but
  for bulk records. Unless this requirement exists - this API can be ignored.

### Burn APIs
This API is specifically for burn transactions that are initiated outside the
Epic ecosystem. Typical scenario: Client has their own burn funnels, users will
spend points on those burn funnels. 

``` POST /api/v1/evaluations/burn?access_token={{user_access_token}}```

This will evaluate the burn transaction and deduct the points from that user's
wallet. Appropriate error message will the sent if there is insufficient balance
etc.

### Wallet APIs
These are internal APIs for Epic LMS <-> Epic App Wallet communication. These
are not intended for any outside communication.

List of all customer wallets for a particular client

``` GET /api/v1/wallets?issuer_id={{issuer_id}}&access_token={{user_access_token}}```

This will give a list of all customer wallets that the issuer has

Authorize a specific wallet and obtain a wallet token

``` POST /api/v1/wallets/authorize?access_token={{user_access_token}}```

This will give a Wallet Access Token for that particular wallet. 

Get Specific details about a wallet

``` GET /api/v1/wallets/specific_wallet?id=1&access_token={{user_access_token}}&wallet_access_token={{wallet_access_token}}```


