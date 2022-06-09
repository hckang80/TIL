# 목차

## 개발하며 쌓인 나의 기억 모음

<details>
  <summary>REGEX</summary>
  
  ```js
  // 비밀번호(대소문자, 숫자, 특문 포함 8자리 이상)
  /^(?=.*[a-zA-z])(?=.*[0-9])(?=.*[`~!@#$%^&*()-_=+[{\]}\\|;:'",<.>/?]).{8,}$/
  ```
  
  ```js
  // 연결 가능한 텍스트를 링크 요소로 변경
  const replaceURLWithHTMLLinks = (str) => {
    const regURL = new RegExp('(http|https|ftp|telnet|news|irc)://([-/.a-zA-Z0-9_~#%$?&=:200-377()]+)', 'gi')
    return str.replace(regURL, "<a href='$1://$2' target='_blank' rel='noreferrer noopener'>$1://$2</a>")
  }
  ```

  ### 특수기호
  - \d : 숫자만
  - \D : \d와 반대
  - \w : 영문 대소문자 + 숫자 + 언더바
  - \W : \w 이외의 문자
  - \s : 공백 문자
  - \S : \s 이외의 문자
</details>

<details>
  <summary>CSS Tricks</summary>
  
  ```css
  /* Hidden cursor only */
  input {
    color: transparent;
    text-shadow: 0 0 0 #000;
  }
  ```
  
  ```html
  <!-- Rating Stars -->
  <div class="ratings">
    <div class="empty-stars"></div>
    <div class="full-stars" style="width:70%"></div>
  </div>
  ```

  ```css
  .ratings {
    position: relative;
    vertical-align: middle;
    display: inline-block;
    color: #b1b1b1;
    overflow: hidden;
  }
  .full-stars {
    position: absolute;
    left: 0;
    top: 0;
    white-space: nowrap;
    overflow: hidden;
    color: #fde16d;
  }
  .empty-stars:before, .full-stars:before {
    content:"\2605\2605\2605\2605\2605";
    font-size: 14pt;
  }
  .empty-stars:before {
    -webkit-text-stroke: 1px #848484;
  }
  .full-stars:before {
    -webkit-text-stroke: 1px orange;
  }
  ```
</details>

<details>
  <summary>Mobile Issues</summary>

  ### iOS
  - 3D transform에서 z-index가 제대로 인식되지 않는 경우
  ```css
  .selector {
    transform-style: preserve-3d;
    transform: translateZ(-1000px);
  }
  ```
</details>

<details>
  <summary>Generator</summary>

  ```js
  // Generate a random ID
  const id = Math.random().toString(36).slice(2)
  console.log(id) // p0ambi8jhik
  ```
  
  ```js
  // Shuffle an array
  const arr = ['A', 'B', 'C', 'D', 'E']
  const shuffled = [...arr].sort(() => Math.random() - 0.5)
  console.log(shuffled) // ['D', 'A', 'B', 'C', 'E']
  ```
  
  ```js
  // Object deep search
  const objectDeepSearch = ({ model = {}, path = '' }) => {
    const list = path.split('.')
    const key = list.pop()
    const pointer = list.reduce((object, prop) => {
      if (object[prop] === undefined) object[prop] = {}
      return object[prop]
    }, model)
    const result = { pointer, key }
    return result
  }

  const model = {
    name: {
      first: 'Hee-chang'
    }
  }
  console.log(objectDeepSearch({ model, path: 'name.first' })) // { pointer: { first: 'Hee-chang' }, key: 'first' }
  ```
  
  ```js
  // Compact Number
  const compactNumber = (value) => {
    const suffixes = ['', 'k', 'm', 'b', 't']
    const suffixNum = Math.floor(('' + value).length / 3)
    let shortValue = parseFloat((suffixNum ? value / Math.pow(1000, suffixNum) : value).toPrecision(2))
    !(shortValue % 1) && (shortValue = shortValue.toFixed(1))
    return shortValue + suffixes[suffixNum]
  }
  console.log(compactNumber(100000)) // '0.1m'
  ```
  
  ```js
  // Ordinal Suffix
  const ordinalSuffix = (number) => {
    const j = number % 10
    const k = number % 100
    let suffix = 'th'
    j === 1 && k !== 11 && (suffix = 'st')
    j === 2 && k !== 12 && (suffix = 'nd')
    j === 3 && k !== 13 && (suffix = 'rd')
    return `${number}${suffix}`
  }
  console.log(ordinalSuffix(1)) // '1st'
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

<details>
  <summary>Optimize to load the Web font (feat. axios)</summary>
  
  ```js
  const cssHref = 'css/webfont.css'

  const isFileCached = (href) => {
    return localStorage.font_css_cache &&
      (localStorage.font_css_cache_file === href)
  }

  const injectRawStyle = (text) => {
    const style = document.createElement('style')
    style.innerHTML = text
    document.getElementsByTagName('head')[0].appendChild(style)
  }

  const requestFontCssToServer = async () => {
    const data = await fetch(`${location.origin}/${cssHref}`).then(res => res.text())
    injectRawStyle(data)
    localStorage.font_css_cache = data
    localStorage.font_css_cache_file = cssHref
  }

  const injectFontsStylesheet = () => {
    if (isFileCached(cssHref)) return injectRawStyle(localStorage.font_css_cache)
    requestFontCssToServer()
  }

  if (localStorage.font_css_cache) return injectFontsStylesheet()
  addEventListener('load', injectFontsStylesheet, false)
  ```
</details>

<details>
  <summary>Resize to Base64</summary>

  ```js
  const resize = (imageFile, maxSize = { width: 800, height: 800 }) => {
    return new Promise((resolve, reject) => {
      const image = new Image()
      image.onload = () => {
        const canvas = document.createElement('canvas')
        let width = image.width
        let height = image.height
        const horizontalType = width > height
        if (horizontalType) {
          if (!(width > maxSize.width)) return
          height *= maxSize.width / width
          width = maxSize.width
        } else {
          if (!(height > maxSize.height)) return
          width *= maxSize.height / height
          height = maxSize.height
        }
        canvas.width = width
        canvas.height = height
        canvas.getContext('2d').drawImage(image, 0, 0, width, height)
        const photoFile = canvas.toDataURL('image/png')
        resolve(photoFile)
      }
      image.src = imageFile
    })
  }

  const toBase64 = (file, resizable = true, maxSize = { width: 800, height: 800 }) => {
    const reader = new FileReader()
    reader.readAsDataURL(file)
    return new Promise((resolve, reject) => {
      reader.onerror = error => {
        reject(error)
      }
      reader.onloadend = async (event) => {
        if (!resizable) return resolve(event.target.result)
        resolve(await resize(event.target.result, maxSize))
      }
    })
  }
  ```
</details>

<details>
  <summary>Reference</summary>
  
  - [User Agent 등의 속성 출력](https://jsfiddle.net/xkfdnwzq/show)
</details>

## 컴퓨터 공학

- [180110.md](./_180110.md)  
  리눅스의 역사 및 git command
- [180112.md](./_180112.md)  
  웹 개발 패턴의 변화, Web Browser, URI, URL, URN

## 기타

- [220609.md](./_220609.md)  
  클린 아키텍처
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