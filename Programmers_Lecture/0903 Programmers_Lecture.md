# 강의 정리 🚀
___

> 2021.09.03 SpringBoot Part

## 공부한 내용

- ### 모든 것은 공식문서와 함께!!! ###

- ### Autoconfiguration ###
    - @SpringBootApplication 어노테이션을 보면 @EnableAutoConfiguration 어노테이션이 있다. 이 안을 보면, @Import(AutoConfigurationImportSelector.class)가 있는데 이를 통해서 여러 AucoConfiguration 클래스들을 선택적으로 적용되게 해준다. (getAutoConfigurationEntry 메소드로 인해서)

- ### 실습 및 어노테이션의 원리 이해 ###