# Initialization

## Initializing the required databases `_users`, `_replicator` and `_global_changes`.

```bash
# https://github.com/apache/couchdb/issues/1354#issuecomment-393389348

curl -X PUT http://christian:pw@localhost:5984/_users
curl -X PUT http://christian:pw@localhost:5984/_replicator
curl -X PUT http://christian:pw@localhost:5984/_global_changes
```

## Setting `chttpd/bind_address`

```bash
# https://docs.couchdb.org/en/stable/config/intro.html#setting-parameters-via-the-http-api
# `node` equals the name of the docker service: 'couchdb'
# `host` equals the `nodename`-env in docker compose: 'alpha'
# In order the check available notes: see `_membership`-api in codeblock above.
curl -X PUT 'http://christian:pw@localhost:5984/_node/<node>@<host>/_config/chttpd/bind_address' -d '"0.0.0.0"'

# authentication handlers

curl -X GET 'http://christian:pw@localhost:5984/_node/couchdb@alpha/_config/chttpd/authentication_handlers' --user christian

curl -X PUT 'http://christian:pw@localhost:5984/_node/couchdb@alpha/_config/chttpd/authentication_handlers' -d '"{chttpd_auth, cookie_authentication_handler}, {chttpd_auth, default_authentication_handler}"'
```

## Cluster: Managing nodes.

```bash
# cluster: node management
curl -X GET "http://localhost:5984/_membership" --user christian

# cluster delete a node
## cluster: read node revision
curl -X GET "http://localhost:5984/_node/_local/_nodes/<node>@<host>" --user christian
## cluster: delete a node
curl -X DELETE "http://localhost:5984/_node/_local/_nodes/<node>@<host>?rev=<revision>" --user christian
```