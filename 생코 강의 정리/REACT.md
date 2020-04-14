#

# npm을 이용해서 create react app 설치

npm(플레이 스토어와 비슷한 역할, node의 플레이 스토어 (모듈 다운로더))을 사용하기 위해서 node 설치

설치후 cmd 창에 node -v로 버전 확인

확인 후 npm install -g create-react-app으로 create react app 설치

npx는 딱 한번 만 설치하여 실행 후 삭제(장점 : 공간 낭비 x, 단점 : 설치 필요시 매번 다시 다운로드 필요)

# 프로젝트 샘플 웹앱 실행
create react app 설치가 끝났으면 프로젝트 폴더 생성(react-app으로 생성 함)

그 후 폴더 경로로 가서 create-react-app . 을 실행하면 프로젝트에 필요한 것들이 자동으로 설치

그 후 터미널 열기로 터미널을 열어 npm run start를 치면 앱 실행

# JavaScript 코딩하는 법

폴더 구조 

public - 정적파일(html, txt, png, ico 등)
src - 주요 소스 파일(.js(react적인))

index.html
```
<body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
</body>
```

아래의 id="root"로 여러 js를 렌더링

index.js
```
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import * as serviceWorker from './serviceWorker';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

serviceWorker.unregister();
```

import App from './App'; ( = ./App.js)

으로 App.js를 선언 후에 <App />로 App.js의 내용 적용

또한 document.getElementById('root') js문법을 이용해 index.html의 <div id="root">에 index.js를 사용한다..

App.js

```
import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
      </div>
    );
  }
}

export default App;
```

react의 Component중 하나로 function 방식과 class 방식중 class 방식을 사용한 것이다.

index.js 에 </App>에 저 내용이 들어가게 된다.

export를 통해 다른 파일에서도 사용할 수 있게 해준다.

# CSS 코딩하는 법

index.js에 보면 아래와 같은 코드가 있다.
```
import './index.css';
```
이 코드처럼 경로에 index.css(.css)라는 파일이 존재하면 index와 관련된 css 속성들이 적용이 된다.

# 배포하는 법

터미널에 npm run build라고 치면 build라는 폴더가 생기며 build(배포)용 파일들을 생성한다.(보안적, 용량적으로 불필요한 것들이 제거된 파일)

이후 

npm serve -s build를 치면 배포용 파일들을 이용해 임시 서버에 배포를 해준다.

# 컴포넌트 생성

## 리액트가 없다면?

아래는 리액트가 적용되지 않은 pure.html이다.

```
<html>
    <body>

        <header>
            <h1>WEB</h1>
            world wide web!
        </header>

        <nav>
            <ul>
                <li><a href="1.html">HTML</a></li>
                <li><a href="2.html">HTML</a></li>
                <li><a href="3.html">JavaScript</a></li>
            </ul>
        </nav>

        <article>
            <h2>HTML</h2>
            HTML is HyperText Markup Language.
        </article>
    </body>
</html>
```

하지만 만약 코드를 변경해야 하면 위 페이지와 비슷한 페이지가 많은 경우 nav 등을 고치기 힘들다 또한 반복적인 코드를 많이 쓰게 된다 따라서 아래 처럼 일부 코드가 다른 코드로 바뀔 수 있다면 좋을 것이라 생각이 된다.

```
    <header>
        <h1>WEB</h1>
        world wide web!     ---> <Subject></Subject>
    </header>
```

## 컴포넌트 만들기

App.js에 아래와 같이 Subject 클래스를 만든다.

```
import React, { Component } from 'react';
import './App.css';

class Subject extends Component {
 render(){
   return (
    <header>
    <h1>WEB</h1>
    world wide web!
  </header>
   );
 }
}

class App extends Component {
  render() {
    return (
      <div className="App">
      </div>
    );
  }
}

export default App;
```

그 후 아래의 App의 <div>코드내에 우리가 선언한 <Subject></Subject> 컴포넌트를 선언해서 사용해준다.

```
class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject></Subject>
      </div>
    );
  }
}
```

이러면 pure.html의

```
<html>
    <body>
        <header>
            <h1>WEB</h1>
            world wide web!
        </header>
    </body>
</html>
```
와 같은 기능을 한다.

다만, react는 단 하나의 최상위 객체를 가져야만 한다.

# Props 사용법

위에서 Component를 통해 복잡성을 줄이고 간편화 시켰다. 하지만 위의 방법으론 Subject를 사용했을 때 언제나 같은 결과만을 보여준다.

이에 react는 태그의 속성(attr) 값처럼 같은 태그일 지라도 차이점을 주는 것으로 Props를 사용하게 된다.

즉, 동적으로 변하는 Component를 만들 수 있게 된다.

props를 사용하는 방법은 아래와 같다.

```
class Subject extends Component {
 render(){
   return (
    <header>
      <h1>{this.props.title}</h1>
      {this.props.sub}
    </header>
   );
 }
}

class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject title="WEB" sub="world wide web!"></Subject>
        <Toc></Toc>
        <Content></Content>
      </div>
    );
  }
}
```

이처럼 <Subject>태그 내에 속성으로 줄 이름과 내용을 입력하고 위쪽에 적용된 Component내에 `{this.props.속성이름}`의 형식으로 사용한다.

# 컴포넌트 파일로 분리하기

지금까진 App.js 파일 내에 여러 개의 컴포넌트 Class를 생성하여 사용하였다. 하지만 컴포넌트 개수가 많아지면 파일이 알아보기 힘들고 유지보수가 안좋아진다.
따라서 component만의 폴더를 만들고 파일을 분할해주는 것이 좋다.

src 폴더 밑에 components라는 폴더를 만들어준다.

이후에 Toc의 내용을 분리하기 위해 components 폴더 밑에 Toc.js라는 파일을 생성하고 App.js의 Toc 코드를 이동시킨다.

하지만, 이동된 Toc.js에는 Component에 대해서 알려주지 않았기 때문에 사용하기 위해선 아래와 같이 Component를 import 해주어야 한다.

```
import React, {Component} from 'react';
```

또한, 다른 외부 파일에서 Toc를 사용할 수 있어야 하기에 파일 마지막에 export 역시 해주어야 한다.

```
export default Toc;
```

그 이후엔 App.js의 Toc 코드를 지우고 TOC.js의 코드를 사용하기 위해 import 해준다.

```
import Toc from "./components/TOC"
```

# State

props - 사용자에게 컴포넌트를 조작 가능하게 만듬

state - 사용자가 알 필요 없는 컴포넌트 내부의 내용

그래서 App.js는 TOC와 같은 Component가 어떻게 동작하는 지 알 필요가 없어진다.

코드로 적용을 하자면 지금까지의 우리 코드는 하드코딩이 되어있었다. props를 이용했다고 하더라도 props 속성을 하드코딩을 하여 줬다.

```
class App extends Component {
  render() {
    return (
      <div className="App">
        <Subject title="WEB" sub="world wide web!"></Subject>
        <TOC></TOC>
        <Content title="HTML" desc="HTML is HyperText Markup Language."></Subject>
      </div>
    );
  }
}
```

이를 State를 이용해서 변경해 보겠다.

### Constructor

Constructor는 컴포넌트 실행시 제일 먼저 실행되는 것으로 주로 초기화를 담당한다.
우리는 각 컴포넌트가 그려지기 전에 props에 값을 추려하므로 이를 이용해 props 값을 초기화 한다.

```
class App extends Component {
  constructor(props){
    super(props);
    // state 초기화
    this.state = {
      subject: {title:'WEB', sub:'World Wide Web!'},
      contents:[
        {id:1, title:'HTML', desc:'HTML is for information'},
        {id:2, title:'CSS', desc:'CSS is for design'},
        {id:3, title:'JavaScript', desc:'JavaScript is for interactive'}
      ]
    }
  }
  render() {
    return (
      <div className="App">
        <Subject title="WEB" sub="world wide web!"></Subject>
        <TOC></TOC>
        <Content title="HTML" desc="HTML is HyperText Markup Language."></Subject>
      </div>
    );
  }
}
```

그 후에 이를 이용해서 props 값을 state 값으로 주려면 아래와 같이 하면 된다.

```
render() {
  return (
    <div className="App">
      <Subject title={this.state.subject.title} sub={this.state.subject.sub}></Subject>
      <TOC data={this.state.contents}></TOC>
      <Content title="HTML" desc = "HTML is HYperText Markup Language"></Content>
    </div>
  );
}
```