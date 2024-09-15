Journey for new user:

1. setup domain address settings:
    # for example { domain: pixiee.io, sso_domain: sso, finance_domain: wallet }
    - TXT record, usso-challenge.{sso_domain} -> {random generated uuid}
    - CNAME record, {sso_domain}.{core_domain} -> relay.usso.io
    - TXT record, ufaas-challenge.{finance_domain} -> {random generated uuid}
    - CNAME record, {finance_domain}.{core_domain} -> relay.ufaas.io

2. Create USSO account
    - Add domain to usso domains
    - Create user account for admin in usso on the business usso.io
    - Create business for domain {sso_domain}.{core_domain} with created user_id
    - Create user for admin on the new host
    - check login methods
    - Check login

3. Create UFaaS account
    - Add domain to ufaas domains
    - Create business on ufaas core
    - Create business on ufaas api-os
    # install extension (zarinpal)
        - Create business on ufaas extension (setup secrets and config)
        - in api-os: Create installed object in api-os for extension and business
        - in core: setup extension wallets
            - income wallet
            - extension wallet
    - check sample transaction on the system


برای استفاده videm
- دو تا آدرس مهدی می‌ده که حامد ست کنه
- بعد بیزنس videm را در core می‌سازیم
- در اکستنشن منیجر بیزنس videm را می‌سازیم
- زرین پال را نصب می‌کنیم
-- آبجکت install را بسازیم
-- در زرین‌پال بیزنس را بسازیم 
--یک sso برای videm نصب کنیم. sso ی videm را چک کنیم.
- کیف پول‌های مربوطه را بسازیم:
-- خود  videm
-- income wallet
-- zarinpal wallet