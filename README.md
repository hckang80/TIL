# 목차

## 그날의 기억
<details>
  <summary>paramsSerializer For the GET parameters</summary>
  
  ```js
    // params: { id: [1, 2] } => api-end-point?id=1&id=2
    axios.defaults.paramsSerializer = (paramObj) => {
      const params = new URLSearchParams()
      for (const key in paramObj) {
        if (Array.isArray(paramObj[key])) {
          for (let i = 0; i < paramObj[key].length; i++) {
            params.append(key, paramObj[key][i])
          }
        } else {
          params.append(key, paramObj[key])
        }
      }
      return params.toString()
    }
  ```
</details>

- [remembers.md](./_remembers.md)  
  회사업무, 개발그룹 등을 통해 얻은 기억 모음


## 컴퓨터 공학

- [180110.md](./_180110.md)  
  리눅스의 역사 및 git command
- [180112.md](./_180112.md)  
  웹 개발 패턴의 변화, Web Browser, URI, URL, URN

## HTML, CSS

- [180115.md](./_180115.md)  
  World Wide Web

- [180116.md](./_180116.md)  
  CSS3 Design

- [180117.md](./_180117.md)  
  웹접근성, 아웃라인

- [180118.md](./_180118/)  
  샘플 사이트 마크업

- [180119.md](./_180119.md)  
  background, animation

  ​

## Javascript

- [180129.md](./_180129.md)  
  JS History


- [180130.md](./_180130.md)  
  자료형과 변수
- [180201.md](./_180201.md)  
  제어문, object, function
- [180202.md](./_180202.md)  
  Scope, this, ESlint
- [180205.md](./_180205.md)  
  Built-in Object, String, Date
- [180206.md](./_180206.md)  
  Number, Math, RegExr
- [180208.md](./_180208.md)  
  Array, Execution Context, Closure
- [180219.md](./_180219.md)  
  DOM, Event
- [180220.md](./_180220.md)  
  고차함수 등 Array 두번째 시간
- [180222.md](./_180222.md)  
  Ajax - JSON, XMLHttpRequest
- [180223.md](./_180223.md)  
  REST API



## ES6

- [180226.md](./_180226.md)  
  let, const, Arrow function

- [180227.md](./_180227.md)  

  기본 파라미터 초기값, Rest 파라미터, Spread 연산자, 디스트럭처링, 클래스

- [180301.md](./_180301.md)

  Class, Promise, Module

- [180302.md](./_180302.md)

  Websocket

- [180305.md](./_180305.md)

  Node.js, Module, Express

  ​

## TypeScript

- [180308.md](./_180308.md)

특장점, 클래스, 인터페이스, 제네릭

- ​

  ​

## Angular

- [180309.md](./_180309.md)

특징 및 설치와 실행 방법