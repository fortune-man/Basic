[참고](https://www.inflearn.com/course/%EC%8A%A4%ED%94%84%EB%A7%81-mvc-1/dashboard)
- 모든 저작권은 해당 강사님께 있습니다

---

Goal

- 웹 애플리케이션 개념에 대해 설명할 수 있다


---


# 웹서버, 웹 애플리케이션 서버란?



## 웹 서버

- HTTP 기반으로 동작하는 서버
- 정적 리소스(index.html, css, js) 제공, 기타 부가기능
- 예) NGINX, APACHE

>클라이언트 <-> 서버 간 웹 통신의 기반은 HTTP
- HTML, TEXT
- IMAGE, 음성, 영상, 파일
- JSON, XML (API)
- 서버간 데이터 통신의 대부분 경우
- 지금은 HTTP 시대

---

## WAS (웹 애플리케이션 서버)

- HTTP 기반하는 서버 + `로직까지`

- 웹 서버 기능 ( 정적 리소스 제공 )
- 코드 실행을 통한 로직 수행 (큰 차이점)
    - 동적 HTML, HTTP API (JSON)
    - 서블릿,  JSP, 스프링 MVC
    - 예) 톰캣, 제티, undertow
### 웹 서버 vs WAS 차이는?
- 정적 리소스(웹서버) vs 로직까지(WAS)
- 모호한 경계점
    - 웹 서버도 프로그램을 실행하는 기능 포함하기도함
    - WAS도 웹 서버의 기능 제공
- 자바의 경우
    - 서블릿 컨테이너 제공하면 WAS로
        - 서블릿 없이 자바 코드를 그대로 실행해주는 서버 프레임워크도 있음
    - WAS는 애플리케이션 코드를 실행하는데 더 특화

### 실무 용도
- WAS가 정적 리소스 + 로직 모두 담당하면? -> 과부하
- 중요한 비즈니스 로직이 정적 리소스 때문에 수행이 안되면? -> 안된다
- WAS 장애 전파 -> WAS 장애시 오류 화면도 노출 안됨

### 보통 회사들 구성 - WEB, WAS, DB
- 일단 정적 리소스는 웹 서버가 처리
    - 장점 : 웹은 정적 리소스만 처리하고 힘들면 넘김
    - 정적 리소스만 제공하는 웹 서버는 잘 죽지 않음
- 동적인 처리가 필요하면 WAS에 요청을 위임
    - 장점 : WAS는 중요한 앱 로직 처리만 전담 가능
    - 단점 : WAS는 잘 죽음
        - WAS, DB 죽을 때  WEB 서버가 오류 화면 HTML 렌더링 가능
    - 요즘엔 정적 리소스 캐시하는 CDN 이란 것도 있다고..
    - [참고](https://velog.io/@heka1024/CDN%EA%B3%BC-%EC%BA%90%EC%8B%9C-%EC%84%A4%EC%A0%95%EC%9C%BC%EB%A1%9C-%EC%A0%95%EC%A0%81%ED%8C%8C%EC%9D%BC%EC%9D%84-%EB%B9%A0%EB%A5%B4%EA%B2%8C)
    - 만약 API 서버만 제공을 하면 뭐다?
        - 굳이 웹 서버가 필요하지 않을 수도 있다
    - 데이터만 주고 받을 때는 WAS 서버만 구축해도 괜찮을 수 있다





---

서블릿과 멀티 스레드
서블릿
HTTP 데이터를 WAS에 전달하면 어떤 일이 일어날까?
생각보다 할 일이 엄청 많다

개발자 혼자 이걸 다하면 요래저래 엄청 비효율적이고 힘들다
개발자가 비즈니스 로직에만 집중할 수 있도록 만들어줘야할 필요가 있었는데, 이 때 등장한게 서블릿

서블릿 특징

```java
@WebServlet(name="helloservlet", urlpatterns="/hello")
public class HelloServlet extends HttpServlet {
@Override
protect void service(HttpServletRequest request, HttpServletResponse response) {
// 비즈니스 로직
}
```

- urlPatterns(/hello)의 URL이 호출되면 서블릿 코드가 실행됨
- HTTP 요청 정보를 편리하게 사용할 수 있는 HttpServletRequest를 지원
- HTTP 응답 정보를 편리하게 제공할 수 있는 HttpServletResponse를 지원
- 요점은 개발자가 HTTP 스펙을 편하게 써먹기 위해 서블릿이 등장
HTTP 요청 응답 흐름
HTTP 요청시

- WAS는 Request, Resopnse 객체를 새로 만들어서 서블릿 객체를 호출
- 개발자는 Request 객체에서 HTTP 요청 정보를 편리하게 꺼내서 사용
- 개발자는 Response 객체에서 HTTP 응답 정보를 편리하게 입력
- WAS는 Response 객체에 담겨있는 내용으로 HTTP 응답 정보를 생성

---

# HTML, HTTP API, CSR, SSR

---

# 자바 웹 히스토리

