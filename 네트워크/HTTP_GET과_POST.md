# HTTP GET과 POST

## HTTP 메서드

HTTP 메서드란 클라이언트가 `웹 서버에게 사용자 요청의 목적이나 종류를 알리는 수단`이다.

![image](https://user-images.githubusercontent.com/97162920/174619702-21675692-c7a1-45d7-9c93-1066c3c49cc4.png)
## GET

클라이언트에서 서버에게 `정보를 요청`하기 위해 사용되는 메서드

요청하는 정보가 HTTP의 `header에 담겨 전송`된다. 즉, url의 ? 뒤에 데이터가 붙어서 요청된다.

url 글자수에 제한이 있기 때문에 GET 요청의 `데이터 크기에도 제한`이 있을 수 밖에 없다.

데이터가 url에 그대로 노출되기 때문에 POST 요청에 비해 `보안에 취약`하다.

`idempotent`하다(멱등성) - 같은 요청을 여러번 보내도 매번 같은 응답이 온다. →can be cached

## POST

클라이언트에서 서버로 리소스를 새로 생성하거나 업데이트하기 위해 사용되는 메서드

요청하는 정보가 HTTP의 `body에 담겨 전송`된다. 데이터 크기의 제한이 없다.

idempotent하지 않다. 요청을 보낼 때 마다 같은 응답이 온다는 보장이 없다. → not cached


---

참고

[[HTTP] HTTP Method 정리 / GET vs POST 차이점 :: Code Playground (tistory.com)](https://im-developer.tistory.com/166)
