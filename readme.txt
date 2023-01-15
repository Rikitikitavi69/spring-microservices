ch11
Acquiring access token using the authorization code grant flow:
1. browser: 
https://localhost:8443/oauth2/authorize?response_type=code&client_id=reader&redirect_uri=https://my.redirect.uri&scope=product:read&state=35725
or
https://localhost:8443/oauth2/authorize?response_type=code&client_id=writer&redirect_uri=https://my.redirect.uri&scope=product:read+product:write&state=35725
2. 
$ CODE=<copy-paste code from prev link redirect>
$ curl -k https://reader:secret@localhost:8443/oauth2/token \
 -d grant_type=authorization_code \
 -d client_id=reader \
 -d redirect_uri=https://my.redirect.uri \
 -d code=$CODE -s | jq .
or 
curl -k https://writer:secret@localhost:8443/oauth2/token -d grant_type=authorization_code -d client_id=writer -d redirect_uri=https://my.redirect.uri -d code=$CODE -s | jq .

use:
curl https://localhost:8443/product-composite/999 -k -H "Authorization: Bearer $ACCESS_TOKEN" -X DELETE -i