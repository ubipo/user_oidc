# user_oidc

OIDC connect user backend for Nextcloud

## General usage
See [Nextcloud and OpenID-Connect](https://www.schiessle.org/articles/2020/07/26/nextcloud-and-openid-connect/)
for a proper jumpstart.

## Commandline settings
The app could also be configured by commandline.

### Provider entries
Providers are located by provider identifier.

To list all configured providers, use:
```
sudo -u www-data php /var/www/nextcloud/occ user_oidc:provider
```

To show detailed provider configuration, use:
```
sudo -u www-data php /var/www/nextcloud/occ user_oidc:provider demoprovider
```

A provider is created if none with the given identifier exists and all parameters are given:
```
sudo -u www-data php /var/www/nextcloud/occ user_oidc:provider demoprovider --clientid="WBXCa003871" \
    --clientsecret="lbXy***********" --discoveryuri="https://accounts.example.com/openid-configuration"
```

To delete a provider, use:
```
sudo -u www-data php /var/www/nextcloud/occ user_oidc:provider:remove demoprovider
  Are you sure you want to delete OpenID Provider demoprovider
  and may invalidate all assiciated user accounts.
```
To skip the confirmation, use `--force`.

***Warning***: be careful with the deletion of a provider because in some setup, this invalidates access to all
NextCloud accounts associated with this provider.


### ID4me option
ID4me is an application setting switch which is configurable as normal Nextcloud app setting:
```
sudo -u www-data php /var/www/nextcloud/occ config:app:set --value=1 user_oidc id4me_enabled
```

## Building the app

Requirements for building:
- Node.js 14
- NPM 7
- PHP
- composer

The app uses [krankerl](https://github.com/ChristophWurst/krankerl) to build the release archive from the git repository. 
The release will be put into `build/artifacts/` when running the `krankerl package`.

The app can also be built without krankerl by manually running:

```
composer install --no-dev -o
npm install
npm run build
```
