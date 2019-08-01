# aarhus-kommune-management-documentation

## Endpoints

### Authentication

By `POST`'ing to `/aarhus-kommune-management/authenticate` an OAuth2 token is
returned.

Example request:

```sh
curl https://example.com/aarhus-kommune-management/authenticate \
        --header "content-type: application/x-www-form-urlencoded" \
        --header "Accept: 1.0" \
        --data-urlencode "grant_type=client_credentials" \
        --data-urlencode "client_id=x-IqP7h3AwVnrkibFSUkJagziN0eCFPLjkA8jntJSB-7E" \
        --data-urlencode "client_secret=eqbJ8oOzXp37lNnwTiy3GpA_mWe24Bx-9bcha_O6g_4" \
        --data-urlencode "scope=data:write"
```

Example response:

```json
{
  "token_type": "Bearer",
  "expires_in": 3600,
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJhdWQiOiJJcVA3aDNBd1ZucmtpYkZTVWtKYWd6aU4wZUNGUExqa0E4am50SlNCLTdFIiwianRpIjoiYmY4ZTJkZTExY2ExMmYzMDRkZWJiMmFkMmE2MjAxZDRjMTE1MzExMTEwYmUyMmFmNmQ2ZTU5MjFjODlhMGNhZjdlMmRiZTVmMTVkNTc3ODEiLCJpYXQiOjE1NjQwNDk4NDAsIm5iZiI6MTU2NDA0OTg0MCwiZXhwIjoxNTY0MDUzNDQwLCJzdWIiOiIiLCJzY29wZXMiOlsiZGF0YTp3cml0ZSJdfQ.2trGHd0u7DndO9s-6lX8XF5aUHpuGr8pU4TSNBfFwO7PZNhhdbkx7g3gtZUp7cZ7uI5mNoH2mBZ9kueDnTUbabxYem3XGlzWgah7FlSrz2cflPRwxwtqwvUcP-DRd1jEbKQgE1uwtTLK9-nEW9DFqfcZqH0eO6VnHq3Z9JNY2ll2kUGvWA40hg00vjU11nVWUVGm_2ehMtIPI5GoM_hDLsq6SwxpB7iXHFj-0G4LQYMkERGB0uPFz0Cfze9MT_drwhcz4ZFvT5jA0Gu7vsQfC6pXZ7GnlmRIj1k0eZgEFBG7DLspaewcUaw7ZIgMaJECw1fxFL9DZTvVdp7NWwWUqA"
}
```

@TODO: Should we (also/instead) support simple authentication by just using an
API token in a request header, e.g. `curl --header "authentication: Token …`?
This will make it much simpler to use the api.

### Users

#### Get users

`GET /aarhus-kommune-management/users`

Example request:

```sh
curl http://example.com/aarhus-kommune-management/users' --header "authorization: Bearer «access_token from result above»"
```

Example response:

```json
{
  "data": [
    {
      "uuid": "user:1",
      "email": "admin@example.com"
    },
    {
      "uuid": "user:2",
      "email": "test@example.com"
    }
  ]
}
```

The response must validate against the schema [`users.get.schema.json`](json-schema/schema/users.get.schema.json).

#### Update users

`POST /aarhus-kommune-management/users`

Example request:

```sh
curl http://example.com/aarhus-kommune-management/users' \
        --header "authorization: Bearer «access_token from result above»" \
        --header "content-type: application/json" \
        --data @- <<'JSON'
{
  "users": {
    "update": [
      {
        "uuid": "user:1",
        "name": "Admin Jensen"
      }
    ]
  }
}
JSON
```

The request body must validate against the schema [`users.update.schema.json`](json-schema/schema/users.update.schema.json).

@TODO What must the response look like?

## Implementations

* [https://github.com/rimi-itk/aarhus-kommune-management-bundle](https://github.com/rimi-itk/aarhus-kommune-management-bundle)
* [https://github.com/rimi-itk/aarhus-kommune-management-drupal](https://github.com/rimi-itk/aarhus-kommune-management-drupal)

## Challenges

How do we connect a user that's been created in Drupal to a user from
Brugeropslag? In Loop, users can register via ADFS, but then we don't know their
uuid – or do we?
