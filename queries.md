# Queries

## Query a view 
```bash
# (1) Limit to a specific entry.
# http://<server>:5984/<database>/_design/<designDoc>/_view/<viewName>
curl -X GET 'http://localhost:5984/<database>/_design/views/_view/<view>?key=<identifier>' --user christian

# (2) Group by individual field.
# Retrieve each route with its number of checkpoints.
# https://blog.pablobm.com/2019/07/18/map-reduce-with-couchdb-a-visual-primer/
curl -X GET 'http://localhost:5984/<database>/_design/views/_view/<view>?group_level=1' --user christian
```

```bash
# @see https://simeon-yan-iliev.medium.com/export-import-a-database-with-couchdb-74bfec3831bc
## Write all documents from a database into a json.
curl -X GET 'http://localhost:5984/route/_all_docs?include_docs=true' --user christian > ~/projects/bravo-routes/db_route.json

## Read json and bulk-write into database.
curl -d @~/projects/bravo-routes/db_route.json -H “Content-type: application/json” -X POST http://localhost:5984/route/_bulk_docs
```