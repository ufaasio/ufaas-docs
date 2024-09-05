# Ufaas Apps MVP Scenario

```bash
curl 'wallet.pixiee.io/api/v1/wallets' -H 'content-type: application/json'
```
    --> My wallets

## app endpoints

```bash
curl 'wallet.pixiee.io/api/v1/apps/zarinpal/deposit' \ 
    -H 'content-type: application/json' \ 
    -H 'authorization: Bearer $JWT_SHOP_PIXIEE' \ 
    --data-raw '{"wallet_id": "00000002-0000-0000-0001-000000000001","callback_url":"wallet.pixiee.io/api/v1/"}'
```


```bash
curl 'wallet.videm.com/api/v1/apps/zarinpal/deposit' \ 
    -H 'content-type: application/json' \ 
    -H 'authorization: Bearer $JWT_SHOP_VIDEM' \ 
    --data-raw '{"wallet_id": "00000002-0000-0000-0002-000000000001","callback_url":"wallet.videm.io/api/v1/"}'
```

## installation
1- Permission --> OAUTH2 business usso
2- wallet creation in core
3- business profile creation
    - save wallet_id 
    - get business profile
    - get Zarinpal token and ...

## application journey

0- Permissions
    <> - create 1 wallet for myself (income wallet)
    <> - create 1 wallet for myself (normal wallet)
    - create many wallets for myself
    - create wallet for user
    - create proposal from (self) wallet to user wallet (currency)
    - create proposal from (user) wallet 
    - create holds (currency)

    - release wallet hold (self created)
    - release wallet hold (other created)

    - read wallets amount (currency)
    - read proposals (myself)
    - read proposals (all)
    - read transactions (myself)
    - read transactions (other wallets)
    - read holds (self created)
    - read holds (others created)


1- create application in ufaas-core
    - set base_url (wallet.pixiee.io/api/v1/apps/zarinpal --> ipg.zarinpal.inbeet.tech)
    - set developer id from JWT
    - permission requests (create proposal from ipg wallet)
    - description
    - api doc

2- business Pixiee
    - oauth request (core) --> USSO (permission requests) --> accept (user) --> generate application token to access business data
    - app --> post wallet (user_id) 