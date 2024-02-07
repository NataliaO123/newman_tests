# newman_tests
// pre-authorization script

email=example@example.com
password=123456
url=example.com
response=$(curl -X "POST" \
  $url/auth/signin \
  -H "accept: application/json" \
  -H "Content-Type: application/json" \
  -d "{ \"email\": \"$email\", \"password\": \"$password\" }")
echo "$response"
TOKEN=$(echo "$response" | jq -r '.access_token')
json_data='{  "globalToken": "'"$TOKEN"'",  "url": "'"$url"'" }'

newman run /path/to/collection.json --global-var "globalToken=$TOKEN" --global-var "globalUrl=$url" --global-var "email=$email" --global-var "password=$password" 
