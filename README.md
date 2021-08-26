# 목차

## 개발하며 쌓인 나의 기억 모음

<details>
  <summary>REGEX</summary>
  
  ```js
  // 비밀번호(대소문자, 숫자, 특문 포함 8자리 이상)
  /^(?=.*[a-zA-z])(?=.*[0-9])(?=.*[`~!@#$%^&*()-_=+[{\]}\\|;:'",<.>/?]).{8,}$/

  // 연결 가능한 텍스트를 링크 요소로 변경
  const replaceURLWithHTMLLinks = (str) => {
    const regURL = new RegExp('(http|https|ftp|telnet|news|irc)://([-/.a-zA-Z0-9_~#%$?&=:200-377()]+)', 'gi')
    return str.replace(regURL, "<a href='$1://$2' target='_blank' rel='noreferrer noopener'>$1://$2</a>")
  }
  ```
</details>

<details>
  <summary>CSS Issues</summary>
  
  ```js
  // Comming Soon...
  ```
</details>

<details>
  <summary>Hybrid App Issues</summary>

  ### AOS
  - 인풋 요소에 포커스가 되어도 키패드가 올라오지 않음(앱에서 해결)
  - Alert으로 디버깅이 바로 되지 않음(앱에서 해결)
  ### iOS
</details>

<details>
  <summary>Awesome Pattern</summary>

  ```js
  // Generate a random ID
  const id = Math.random().toString(36).slice(2)
  console.log(id) // p0ambi8jhik

  // Shuffle an array
  const arr = ['A', 'B', 'C', 'D', 'E']
  const shuffled = arr.slice().sort(() => Math.random() - 0.5)
  console.log(shuffled) // ['D', 'A', 'B', 'C', 'E']
  ```
</details>

<details>
  <summary>paramsSerializer For the GET parameters (feat. axios)</summary>
  
  ```js
  // url: 'api-end-point' , params: { id: [1, 2] } => api-end-point?id=1&id=2
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