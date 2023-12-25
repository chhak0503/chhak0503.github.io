spring.security.oauth2.client.provider.kakao.authorization-uri=https://kauth.kakao.com/oauth/authorize
spring.security.oauth2.client.provider.kakao.user-name-attribute=id
spring.security.oauth2.client.provider.kakao.token-uri=https://kauth.kakao.com/oauth/token
spring.security.oauth2.client.provider.kakao.user-info-uri=https://kapi.kakao.com/v2/user/me

spring.security.oauth2.client.registration.kakao.client-name=kakao
spring.security.oauth2.client.registration.kakao.authorization-grant-type=authorization_code
spring.security.oauth2.client.registration.kakao.redirect-uri=http://localhost:8080/login/oauth2/code/kakao
# 카카오 - 내애플리케이션 - 요약정보 - REST API 키
spring.security.oauth2.client.registration.kakao.client-id=클라이언트 아이디

# 카카오 - 내애플리케이션 - 카카오 로그인 - 보안 - Client Secret 
spring.security.oauth2.client.registration.kakao.client-secret=시크릿키
spring.security.oauth2.client.registration.kakao.client-authentication-method=client_secret_post
# 카카오 - 내애플리케이션 - 카카오 로그인 - 동의항목 - 내가 설정한 ID값(자주 바뀌니깐 주의)
spring.security.oauth2.client.registration.kakao.scope=profile_nickname, account_email