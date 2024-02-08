# newman_tests
response=$(curl -X "POST" \
  https://example.com \
  -H "accept: application/json" \
  -H "Content-Type: application/json" \
  -d "{ \"email\": \"example@example.com\", \"password\": \"password123\" }")
echo "$response"
TOKEN=$(echo "$response" | jq -r '.access_token')
json_data='{  "bodyToken": "'"$TOKEN"'",  "url": "https://example.com" }'

newman run /path/to/collection.json --global-var "bodyToken=$TOKEN" --global-var "url=https://example.com" --global-var "email=$email" --global-var "password=$password"
