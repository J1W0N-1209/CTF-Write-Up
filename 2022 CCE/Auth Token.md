Auth Token

사이트에서 guest/guest로 로그인을 합니다.
쿠키값을 보면 JWT 인것을 확인 할 수 있습니다.
base64로 디코딩 한 후에 

{"alg":"HS256","typ":"JWT"}{"id":"guest"} -> guest로 로그인 했을 때 
{"alg":"none","typ":"JWT"}{"id":"admin"} -> 수정 후 저장 !
