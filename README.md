# aarhus-kommune-management-documentation

## Endpoints

### `/aarhus-kommune-management/authenticate`

Two-legged OAuth2 authentication endpoint

```sh
curl https://example.com/aarhus-kommune-management/authenticate \
        --header "content-type: application/x-www-form-urlencoded" \
        --header "Accept: 1.0" \
        --data-urlencode "grant_type=client_credentials" \
        --data-urlencode "client_id=x-IqP7h3AwVnrkibFSUkJagziN0eCFPLjkA8jntJSB-7E" \
        --data-urlencode "client_secret=eqbJ8oOzXp37lNnwTiy3GpA_mWe24Bx-9bcha_O6g_4" \
        --data-urlencode "scope=data:write"
```

### `/aarhus-kommune-management/users`

`GET` users:

```sh
curl http://example.com/aarhus-kommune-management/users' --header "authorization: Bearer «access_token from result above»"
```

Update (`POST`) users:

```sh
curl http://example.com/aarhus-kommune-management/users' \
        --header "authorization: Bearer «access_token from result above»" \
        --header "content-type: application/json" \
        --data @- <<'JSON'
{
 "users": {
  "update": [
   {
    "uuid": "hat-og-briller",
    "name": "Hat & briller"
   }
  ]
 }
}
JSON
```

## Implementations

* https://github.com/rimi-itk/aarhus-kommune-management-bundle
* https://github.com/rimi-itk/aarhus-kommune-management-drupal
