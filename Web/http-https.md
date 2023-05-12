HTTP와 HTTP는 모두 인터넷에서 정보를 주고받을 때 사용되는 프로토콜입니다. <br/>
하지만 HTTPS는 데이터를 암호화하고, 인증서를 통해 웹 사이트의 신원을 확인할 수 있어 더 안전하다는 차이점이 있습니다.

# HTTP

HTTP는 클라이언트와 서버 간 자원을 주고 받을 때 사용하는 프로토콜(통신 규약)로, 요청과 응답으로 이루어져 있습니다.

HTTP는 암호화가 되지 않은 데이터를 전송하기 때문에 개인정보처럼 민감한 정보를 주고받을 때 제3자가 조회할 수 있다는 단점이 있습니다. HTTPS를 이용하면 이런 문제를 해결할 수 있습니다.

# HTTPS

HTTPS는 HTTP에 데이터 암호화가 추가된 프로토콜입니다.

## HTTPS의 장점

1. 암호화된 데이터를 사용하여 보호할 수 있습니다.

<img src='https://tiptopsecurity.com/wp-content/uploads/2017/06/WhatIsHTTPSEncryption.png'/>

([참고](https://tiptopsecurity.com/how-does-https-work-rsa-encryption-explained/))

2. CA 기관에서 인증서를 받기 때문에 접속한 사이트를 신뢰할 수 있습니다.
3. HTTPS를 적용한 사이트는 SEO 순위에 영향을 끼칩니다.

## HTTPS의 연결 과정

HTTPS는 대칭키 암호화 방식과 비대칭키 암호화 방식을 모두 사용하여 빠른 연산속도와 안전성을 얻을 수 있습니다. HTTPS 연결 과정은 다음과 같습니다.

1. 클라이언트가 서버로 연결을 시도하면 서버는 클라이언트에게 인증서를 보냅니다
2. 클라이언트는 CA의 공개키를 이용하여 서버의 신뢰성을 검증한 후 대칭키를 발급하여 서버의 공개키로 암호화한 뒤 서버로 보냅니다
3. 서버는 자신의 개인키(비밀키)를 이용해서 암호화된 대칭키를 복호화합니다.
4. 서버와 클라이언트는 같은 대칭키를 가지고 있으므로 데이터 전달 시 대칭키를 이용하여 복호화를 진행합니다.

### 대칭키 암호화 방식

- 서버와 클라이언트가 하나의 키를 사용하여 암호화와 복호화를 진행하는 방식
- 연산 속도가 빠르지만 키가 노출되면 위험하다는 단점이 있습니다.

### 비대칭키(공개키) 암호화 방식

- 하나의 쌍으로 구성된 공개키와 개인키(비밀키)를 이용하여 암호화와 복호화를 진행합니다.
- 대칭키 암호화 방식보다 안전하지만 연산 속도가 느리다는 단점이 있습니다.

## 서버가 SSL/TLS 인증서를 발급받는 과정

HTTPS를 연결할 때 서버는 일반적으로 CA라 불리는 인증 기관에게 공개키를 전송하여 인증서를 발급받습니다.

1. 서버가 HTTP를 사용하는 어플리케이션에 HTTPS를 적용하기 위해 공개키와 개인키를 발급하여 CA 기관에 공개키를 저장하는 인증서를 발급 요청합니다.

- 이때 인증서에는 서버의 공개키, 정보, CA 기관의 이름 등의 정보가 들어 있습니다.

2. CA 기관은 인증서를 생성하고 CA 기관의 개인키로 암호화하여 서버에게 제공합니다.
3. 서버는 클라이언트에게 암호화된 인증서를 제공합니다.

- 클라이언트의 브라우저에는 이미 CA들의 목록이 들어 있어 서버가 인증서를 보내면 CA의 공개키를 이용하여 인증서를 복호화할 수 있습니다.

> SSL(Secure Sockets Layer)

- 현재 사용되는 TLS의 전신입니다.

> TLS(Transport Layer Security)

- 암호화 및 인증 프로토콜입니다.

# 참고 자료

https://developer.mozilla.org/ko/docs/Web/HTTP/Overview <br/>
https://aws.amazon.com/ko/compare/the-difference-between-https-and-http/<br/>
https://mangkyu.tistory.com/98<br/>
https://tiptopsecurity.com/how-does-https-work-rsa-encryption-explained/<br/>
https://jeong-pro.tistory.com/89<br/>
https://blog.wishket.com/http-그리고-https의-이해/<br/>
https://hyeran-story.tistory.com/159<br/>
https://webactually.com/2018/11/16/http에서-https로-전환하기-위한-완벽-가이드/<br/>
https://aws.amazon.com/ko/what-is/ssl-certificate/<br/>
https://nouljotne.tistory.com/entry/Https화SSL화의-SEO-영향은-개요와-SEO와의-관계를-설명<br/>
https://developers.google.com/search/blog/2014/08/https-as-ranking-signal?hl=ko<br/>
