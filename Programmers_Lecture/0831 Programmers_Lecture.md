# 강의 정리 🚀
___

> 2021.08.31 SpringBoot Part

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### Spring MVC ###
    - Front Controller Pattern
        - Servlet 이 1개
            - Front Controller가 각 컨트롤러에 위임하는 형식을로 진행한다. 
            - 요청은 Front Controller가 받는다.
            - DispatcherServlet 이 Http 요청을 받고, 해당한느 컨트롤러에 요청을 한다.
        
    - 스프링에서는 컨트롤러를 핸드러라고 부른다.
    - 컨트롤러와 서블릿 사이 어댑터 사용
        - 어댑터가 컨트롤러의 타입에 맞게 변환해서 제공
        - 스프링은 이러한 어댑터 핸들러 패턴을 이용한다.
        - 대표적인 RequestMappingHandlerAdapter가 있다.

        ![image](https://user-images.githubusercontent.com/73347933/131448167-b0b8a741-3bcb-4aa3-9396-26e68c653d7a.png)

- ### 강의 실습 ###
    - jstl dependency 추가 이후 실습 진행

    - @EnalbeMvc 사용하면 Spring MVC가 필요한 빈들이 자동으로 등록된다.

