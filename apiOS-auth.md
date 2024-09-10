
3dp ext   ----  OS    ----    Platform    ----    Business    ----    User
                apios ----    UfaaS       ----    pixiee      ----    campaign manager
ipg ext   ----  apios ----    UfaaS       ----    pixiee      ----    campaign manager
                apios ----    Ufiles      ----    pixiee      ----    campaign manager
                ..... ----    SSO         ----    pixiee      ----    campaign manager


SSO (ext, Business)


IPG on --> Private Key
wallet.pixiee.io    --> sso.pixiee.io
wallet.videm.com    --> sso.videm.com
wallet.rentamon.com --> sso.rentamon.com

USSO --> authentication: (login M...) + (3rd party auth)

# What is the permission of ext_E1 on platform_P1 for bus_B1? (--> apiOS_a1)

ext_E1 (sso _B1 token + permission --> installation!)

extension --> (apios / domain! --> platform!)
    ipg: token(core.ufaas.io, business_name!) --> does have permission for bus_name?



# create extension
developer --> api_OS
    create extension {*scopes, *name, privacy-policy, developer_email, ...} -->
    api_OS {api_OS_token} --> sso_platform --> {app_id, app_secret} --> developer
    # api_OS {} --> sso_platform --> {pub_key} --> developer

    implement `base_url/api/v1/apps/[name]/{path}`

# install extension
business_owner --> api_OS
    list extensions --> {names}
    install extension {name} --> api_OS
    
        api_OS register ext {name} --> platform[business] {p_data} # --> wallet creation
        api_OS create business {p_data, zarinpal_token, business_name, sso_platform} --> extension
        # api_OS create extension_user {app_id, app_secret} --> sso_business 
        # api_OS create extension_user {pub_key} --> sso_business 

# use extension
extension --> platform[business]
    extension get access_token {app_id, hash(app_secret), business_name} --> sso_platform {business_name, app_id} --> api_OS { is_installed: true } --> { access_token }
    extension {token} --> platform[business]
