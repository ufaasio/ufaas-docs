IPG Verify:

create proposal
--> redirect to callback

issues:
(done) income wallet
(done) ipg token (SSO) --> sso domain!
(done) redirect to callback


# get all ipg apps (5)
# default merchant_id  (2)
# share revenue percentage app (3)
# add ipg fee (4)
# topup request (1)
# auto callback url
https://core.ufaas.io/api/v1/accounting/wallets/{wid}
https://core.ufaas.io/api/v1/accounting/wallets/{wid}/topup
https://core.ufaas.io/api/v1/apps/zarinpal/purchases/start?amount=1000&description=test&callback_url=https://example.com&wallet_id={wid}
