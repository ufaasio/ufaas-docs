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

<!---
- create 1 wallet for myself (income wallet)
- create 1 wallet for myself (normal wallet)
 -->
- (not yet) create many wallets for myself
- (not yet) create wallet for user
- create proposal from (self) wallet to (user) wallet (currency) (ipg)
- create proposal from (user) wallet to (self) wallet (shop)
- (not yet) create proposal from (user) wallet to (user) wallet (exchange)
- (not yet) create holds (currency) (escrow account)

- (not yet) release wallet hold (self created)
- (not yet) release wallet hold (other created)

- read wallets amount (currency)
- read proposals (myself)
- (not yet) read proposals (all)
- read transactions (myself)
- (not yet) read transactions (other wallets)
- (not yet) read holds (self created)
- (not yet) read holds (others created)

### app permissions
- add item to shop 
- webhook on basket item success


1- create application in ufaas-core
    - set base_url (wallet.pixiee.io/api/v1/apps/zarinpal --> ipg.zarinpal.inbeet.tech)
    - set developer id from JWT
    - permission requests (create proposal from ipg wallet)
    - description
    - api doc

2- business Pixiee
    - core add route application to business faas
    - core create wallets for app + business profile + extra needed data --> app / business
    - oauth request (core) --> (redirect to app) --> USSO (permission requests) --> accept (user) --> sso accept --> app --> core

3- app (ipg) working

app1 (X) 
user --> SSO (app1, X) --> accept or reject

## option 1
(bus) Watch video --> usage (saas) --> reject
(bus) --> (shop) add product to basket {callback: watch video item, webhook: create enrollment for user} ==> (shop) basket 
...
(shop) ==> (ipg_handler) payment link please! {callback: shop basket_id} ==>
(ipg_handler) ==> ipg
ipg ==> (ipg_handler) verify --> ipg
(ipg_handler) ==> (shop) basket_id verify --> (ipg_handler)
    --> call all webhooks of items
        --> (saas) creation verify --> create enroll
(shop) ==> (bus) callback: watch video item --> usage --> accept

## option 2
(bus) Watch video --> usage (saas) --> reject
(bus) ==> (saas) create enrollment {callback: watch video item} --> (shop) add product to basket {webhook: create enrollment for user} ==> (shop) basket_id
...
(shop) ==> (ipg_handler) payment link please! {callback: shop basket_id} ==>
(ipg_handler) ==> ipg
ipg ==> (ipg_handler) verify --> ipg
(ipg_handler) ==> (shop) basket_id verify --> (ipg_handler)
    --> call all webhooks of items
        --> (saas) creation verify --> create enroll
(shop) ==> (bus) callback: watch video item --> usage --> accept