# OAuth 2.0의 흐름에 대해 간단히 설명해주세요

## OAuth?

우리가 Third-Party 서비스를 통해서 캘린더를 활용한다던지, 복사한 글을 SNS에 공유하는 기능을 구현할 수 있다. 이런 기능을 구현하기 위해서 특정 서비스들의 Access 권한이 필요한데 우리가 일반적으로 사용하는 로그인/로그아웃 행위 자체를 다른 서비스에서 사용할 수 있게끔 해준다면, 우리의 소중한 정보가 유출될 수 있는 우려가 있다. 그리고 

구글의 [AuthSub](https://developers.google.com/gdata/docs/auth/authsub?hl=ko)와 같이 각 회사마다 이런 위험한 상황을 방지하는 기술을 개발하였지만, 회사마다 이런 기술들이 달랐기에 각 서비스를 위한 유지보수가 힘들다는 점이 있었다. 그래서 다양한 플랫폼의 특정 사용자 리소스에 접근할 수 있는 권한을 위임할 수 있는 하나의 표준 프로토콜을 만들게 되었고 그것이 바로 OAuth이다.

<br>

## OAuth2.0?

**OAuth2.0**은 인증을 위한 개방형 프로토콜로서 **Third-Party 서비스에게 리소스 소유자를 대신해서 리소스에 제공에 대한 권한을 위임하는 방식.**

<p align="center">
  <img width="300" alt="Untitled (1)" src="https://github.com/wanted-pre-onboarding-team-9/Frontend-CS-Study/assets/49917043/11466c02-9519-485c-96c3-1ca8c35c4d64">

<br>

## OAuth2.0내 4가지 역할

|  | 역할 | ex. |
| --- | --- | --- |
| Resource Owner | 리소스 소유자, 곧 본인. 보호되어있는 자원에 접근할 수 있는 사람. OAuth 프로토콜 흐름에서 Third-Party 서비스에서 인증을 수행하고, 본 서비스에 권한 획득 자격을 부여하는 역할. |  나, 사용자 |
| Client | 보호된 자원을 사용하려고 접근 요청을 하는 애플리케이션 | 넥슨 |
| Resource Server | 사용자의 보호된 자원을 가지고 있는 서버 | Google |
| Authorization Server | 인증/인가를 수행하는 서버로 클라이언트의 접근 자격을 확인해서 Access Token을 발급하고, Access Token을 통해 권한을 부여하는 역할 | Google |

<br>

## OAuth의 동작 과정

|<img width="400" alt="Untitled (1)" src="https://github.com/wanted-pre-onboarding-team-9/Frontend-CS-Study/assets/49917043/df6771fb-9fe7-4a4d-bb67-de5a2416758f"> | <img width="400" alt="Untitled (1)" src="https://github.com/wanted-pre-onboarding-team-9/Frontend-CS-Study/assets/49917043/ec6c5c5e-dd12-4016-ad19-642e38308ca9"> |
| :---: | :---:|
| Google OAuth | Kakao OAuth|


1, 2. **로그인 요청**

`Resource Owner`인 우리가 로그인 요청(Google로 로그인을 클릭)을 보내면, `Client`(넥슨)은 OAuth에서 Authorization과정을 위해서 `Authorization Server`(Google)에 로그인을 요청한다.

1. **로그인 페이지 제공**
    
    사용자는 제공된 Authorization URL으로 이동하여 제공된 페이지(Google)로 이동한다.
    
2. **ID/PW 제공**
    
    제공된 페이지에서 인증과정, 로그인을 수행한다.
    
3. **Authorization Code 제공 및 Redirect URI로 리다이렉트**
    
    제공된 페이지에서 인증을 성공하면 `Authorization Code`가 발급되고, 이를 포함해서 `Authorization Sever`로 Redirect 될 때 함께 전달 받은 Redirect URI를 통해 사용자를 리디렉션 시킨다.
    

6**, 7. Authorization Code와 Access Token 교환**

`Client`는 전달받은 Authorization Code를 `Authorization Sever`로 전달하고, `Authorization Sever`는 리소스 접근 권한을 부여하는 `Access Token`을 발급한다. `Client`는 이 `Access Token`을 저장하고 이후 리소스에 접근이 필요할 때 사용한다.

1. **로그인 성공**
    
    1 ~ 8번 과정을 성공적으로 마치면 `Resource Owner`에게 로그인에 성공했음을 전달한다.
    

9 ~ 12. **Access Token으로 리소스 접근**

`Resource Owner`가 `Resource Server`의 리소스가 필요하다고 요청하면, `Client`는 저장된 `Access Token`을 하여 `Resource Server`의 리소스에 접근하고, `Resource Owner`에게 자사의 서비스를 제공한다.

→ 이후 사용자가 다시 Google 로그인을 사용할 때 재로그인 과정 없이 로그인 가능하다.

<br>

## 앞으로…

OAuth를 사용해본 경험은 한번…? 정도 있지만 이런 과정까지 생각하면서 구현해보진 않아서 이번에도 4가지 역할이 주고받는 과정에만 집중해서 정리했다. OAuth를 다시 한 번 구현하면 Access Token 발급하는 HTTP 요청, Authorization Server URL 쿼리스트링, Redirection URI 등 어떤 리소스들을 주고 받는지 실제로 뜯어보면 좋을 것 같다. 

```
// Authorization URL

https://authorization-server.com/auth?response_type=code
&client_id=29352735982374239857
&redirect_uri=https://example-app.com/callback
&scope=create+delete
```

<br>

## References

https://hudi.blog/oauth-2.0/

https://oauth.net/2/

https://blog.naver.com/mds_datasecurity/222182943542
