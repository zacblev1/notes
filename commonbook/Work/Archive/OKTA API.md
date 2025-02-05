00UP9ZMNFaZ-pKtKqSO24MEvdU4un__xIMnjXOHjoC

curl -i -X GET \
  'https://unlockhealth.okta.com/api/v1/groups?q=West%26limit%3D10&filter=string&after=string&limit=10000&expand=string&search=string&sortBy=lastUpdated&sortOrder=asc' \
  -H 'Authorization: 00UP9ZMNFaZ-pKtKqSO24MEvdU4un__xIMnjXOHjoC'
https://{unlockhealth.okta.com}/api/v1/groups


POST /oauth2/default/v1/token HTTP/1.1  
Host: {yourOktaDomain}  
Authorization: Basic {Base64(clientId:clientSecret)}  
Content-Type: application/x-www-form-urlencodedgrant_type=client_credentials&scope={yourScopes}