# npm, npx 차이

[npm & npx](https://webruden.tistory.com/275)

### NPM

dependency, dev-dependency module을 설치해서 script로 실핼할 수 있음
현재 내가 만들고 있는 프로젝트에 의존적인, 비 의존적인 모듈을 설치하는 것, node_modules에 설치됨

### NPX

프로잭트를 만들어줌, boiler templete처럼 만들어 진 tempelete을 가져옴

이렇게하면 webpack, babel같은 귀찮은 설정들을 미리 해주기 떄문에 매우 유용함

node version이 달라도 가능하고, package에 없는 모듈도 일회용으로 실행할 수 있음
`npx cowsay Hello, wordl!`

<br><br>

# webapck, babel 직접 설정하지 않고 만들기

terminal에 아래 코드 실행
`npx create-react-app movie_app_2021`

<br><br>

# vertural DOM

<App />이란 App.js로 하나의 vertural DOM을 만들 떄 사용함

DOM으로 랜더링 될 경우 소스 코드가 없기 때문에 렌더링 속도가 빠르다고 함

아래와 같이 **componenet**를 만고,

```js
// index.js

reactDOM.render(<App />, document.querySelector(".root"));
```

App component에 채울 요소를 아래와 같이 리턴할 수 있음

Component is return HTML element

아마 이런 개념을 JSX라하고 react에서만 쓰이는 유일한 개념이라고 함

```js
// App.js

import React from "react"

frunction App() {
    return <h1>Hello, world!</h1>
}

export default App
```

<br><br>

# componenet 만들기

아래와 같이 Coponenet를 만들고 실행시킬 수 있다.

```js
// tomato.js
import React from "react";

function Tomato() {
  return <h3>Hello, tomato</h3>;
}

export default Tomato;
```

```js
// Tomato.js
import React from "react";
import Tomato from "./tomato";
function App() {
  return (
    <div>
      <h1>Hello, wordl!</h1>
      <Tomato></Tomato>
    </div>
  );
}

export default App;
```

<br><br>

# Reusable Componenet

아래와 같이 Tomato component를 함수로 만들어서 사용할 수 있고<br>
HTML과 유사한 문법으로 element를 컨트롤 할 수 있음

```js
// App.js

import React from "react";

function Tomato(props) {
  console.log(typeof props); // object
  console.log(props); // {color : "red"}
  return <h3>NOTHNING</h3>;
}
function App() {
  return (
    <div>
      <h1>APP TEST</h1>
      <Tomato color="red"></Tomato>
    </div>
  );
}

export default App;
```

<br><br>

# Destructure Assign으로 Compoenent 작성하기

아래와 같이 reusable한 component를 만들 수 있음

인자로 `Tomato(props, {id})`이렇게 받아올 수 없음 (다른 방법이 있는지는 모루겠음)

```js
// App.js

import React from "react";

function Tomato({ id }) {
  return <h3>NOTHING {id}</h3>;
}
function App() {
  return (
    <div>
      <h1>APP TEST</h1>
      <Tomato id="404"></Tomato>
      <Tomato id="200"></Tomato>
      <Tomato id="666"></Tomato>
    </div>
  );
}

export default App;
```

이게 JSX라고 함

<br><br>

# Rerturn map

map을 사용해서 json, obejct의 값들을 받아올 떄 아래와 같이 작성해서 요소를 만들 수 있음

component는 unique key를 반드시 부여해 줘야 함, key는 react 내부에서 사용하는 유일한 키임

```js
// App.js
import React from "react";

const noticData = [{ id: 404 }, { id: 200 }, { id: 201 }, { id: 202 }];

function Tomato({ id }) {
  return <h3>NOTHING {id}</h3>;
}

function App() {
  return (
    <div>
      <h1>APP TEST</h1>
      // 중괄호를 사용해서 js코드 삽입
      {noticData.map(function (item) {
        // unique id {key = value}가 없으면 에러가 발생함
        return <Tomato key={item.id} id={item.id}></Tomato>;
      })}
    </div>
  );
}

export default App;
```

<br><br>

# prop-types

prop-type는 porperty의 type을 체크하는 기능을 다양하게 제공하고 있음
[prop-types react](https://ko.reactjs.org/docs/typechecking-with-proptypes.html)

`npm install prop-type`

아래와 같이 property의 type를 체크할 수 있음

```js
import React from "react";
import PropTypes from "prop-types";

// function component 보통 class component를 씀
function Tomato({ id, title, rating }) {
  return (
    <div>
      <h3>NOTHING {id}</h3>
      <ul>
        <li>{title}</li>
        <li>{rating}</li>
      </ul>
    </div>
  );
}

// method는 low case
Tomato.propTypes = {
  id: PropTypes.number.isRequired,
  title: PropTypes.string.isRequired,
  rating: PropTypes.number.isRequired,
};

// fake object data
const noticData = [
  { id: 404, title: "test title1", rating: 4.5 },
  { id: 200, title: "test title2", rating: 4.2 },
  { id: 201, title: "test title3", rating: 4.3 },
  { id: 202, title: "test title4", rating: 4.4 },
];

function App() {
  return (
    <div>
      <h1>APP TEST</h1>
      {noticData.map(function (item) {
        return <Tomato key={item.id} id={item.id} title={item.title} rating={item.rating}></Tomato>;
      })}
    </div>
  );
}
export default App;
```

<br><br>

# Class compoenent and state

Class App으로부터 redner()라는 함수를 상속받아서 사용

```js
// App.js
import React from "react";

class App extends Tomamt.Component {
  render() {
    return <h1>First class compoenet</h1>;
  }
}
```

# change mutate state directly

아래 버튼은 작동하지 않음

```js
class App extends React.Component {
  // data will be change
  state = {
    count: 0,
  };
  add() {
    this.state.count += 1;
  }
  minus() {
    this.state.count -= 1;
  }
  render() {
    return (
      <div>
        <h1>First Counting Class Component : {this.state.count} </h1>
        <button onClick={this.add}>add</button>
        <button onClick={this.minus}>minus</button>
      </div>
    );
  }
}
```

`render(){return ( something HTML code.. )}`
이미 화면을 렌더링할 때 코드가 return 됐기 떄문에 위처럼 코드를 적는 다는 것은
**내가 button을 누를 때마다 return해줘**라고 리액트에게 말하는 것과 같음

<br><br>

# setState 사용하기

아래와 같이 state 객체를 만들고 this.setState()메서드를 사용하면 상태변화를 감지할 수 있음

```js
import React from "react";
import PropTypes from "prop-types";

class App extends React.Component {
  // data will be change
  // state 객체의 이름은 임의로 지정할 수 없는 거 같음
  state = {
    count: 0,
  };
  add = () => {
    // this.state.count += 1;
    this.setState((current) => ({
      count: current.count + 1,
    }));
  };
  minus = () => {
    // this.state.count -= 1;
    this.setState((current) => ({
      count: current.count - 1,
    }));
  };
  render() {
    return (
      <div>
        <h1>First Counting Class Component : {this.state.count} </h1>
        <button onClick={this.add}>add</button>
        <button onClick={this.minus}>minus</button>
      </div>
    );
  }
}
```

<br><br>

# arrow function에 대해서 🍎🍉 (진짜 중요.. ) 🍎🍉

결과적으로 아래 코드의 add()는 작동하지만 minus()는 작동하지 않는다.

```js
class App extends React.Component {
  state = {
    count: 0,
  };
  add = () => {
    this.setState();
  };
  minus() {
    this.setState();
  }
}
```

add()에서 this는 React.Component를 가르키고 => React.Component.setState()

minus()에서 this는 minus를 가르키지 떄문 => munus.setState()

arrow function은 this는 function declaration과 다르게 this가 자신을 가르키고 있지 않다.

### implict return (절대적인 반환)

아래의 경우 add(), minus()는 return이 ()에 덮혀있다는 것만 다르다.
하지만 minus()는 작동하지 않는다. 왤까

```js
class App extends React.Component {
  state = {
    count : 0
  }
  add = () => {
    // current = { count : 0 }
    this.setState((current) => ({
      count : current.count + 1
    }))
  }
  minus = () => {
    this.setState((current) => {
      count: current.count - 1,
    });
  divide = () => {
    this.setState((current) => {
      return count : current.count / 2
    });
  }
}
```

arrow function이 객체를 반환하려면 반드시 return을 작성해야 한다.

그게 아니면 내가 작성하는 값을 return하겠다는 뜻으로 ({}) 소괄호로 감싸서 작성할 수 있다. 이를 implict return이라고 한다.

[노마드 코더 댓글 창에 implict return에 대한 토록은 확인해보자 ](https://nomadcoders.co/react-fundamentals/lectures/1553)

생각해보자 function declaration에서 객체를 반환할떄 `return ({key ; value})`이렇게 작성했던 기억을??? 맞나??

arrow function의 this가 항상 자신의 함수를 뜻하지 않기 때문에,

에초에 햇갈리지 않도록 arrow function은 본인을 만든 부모 개체의 this를 의미하게 만들어졌다.

> arrow function의 this, function declaration의 this은 사용처가 다르고 매우 유용하게 쓰이기 떄문에 잘 기억해둬야한다.

# Component life cycle

mounting(component가 생성될 때) , updating(내가만든 함수가 작동될 때), unmounting(component가 죽을 떄),

### constructor()

js에서 class를 만들 때 호출되는 것

### componentDidUpdate()

mount된 component가 업데이트될 때 호출됨

### componentWillUnmount()

component가 죽을 때 호출 됨

setState() => conponent 호출 => render 호출

업데이트 될 때 => componentDidUpdate 실행

# start clone coding

axios를 이용해 .json 파일을 받아오고

컴포넌트를 구분해서 화면에 뿌려줄 거임

코드를 통해 확인 할 수 있음!

# deploy하기 (gh-pages)

터미널에서 gh-pages 설치

`npm install gh-pages`

package.json에 아래와 같이 코드 작성

```json
// package.json
{
  "scripts": {
    "build": "react-scripts build",
    "deploy": "gh-pages -d build",
    "predeploy": "npm run build"
  },
  "homepage": "https://peacepiece7.github.io/react-movie-clone/"
}
```

scripts의 npm run deploy는 predeploy를 실행 종료 후 deploy를 실행 함

"homepage"는 반드시 소문자로 작성해야함!

add file change

# hashRouter Route

아래와 같이 hashrouter를 쓸 수 있음.

hashRouter는 지나가는 경로에 있는 모둔 라우터를 랜더링 하기 떄문에 `exact={true}`옵션이 반드시 필요함.

예를들어 /detail/1123 으로 갈 경우, /, /detail, /detail/1123 세가지 라우터를 뷰포트에 랜더링함

```js
// App.js
import React from "react";
import { HashRouter, Route } from "react-router-dom";
import Home from "./routes/Home";
import About from "./routes/About";
import Navigation from "./components/Navigation";

function App() {
  return (
    <HashRouter>
      <Navigation />
      <Route path="/" exact={true} component={Home} />
      <Route path="/about" component={About} />
    </HashRouter>
  );
}

export default App;
```

# Link to

URL 경로 이동시 화면의 새로고침이 싫다면, 아래와 같이 작성할 수 있음

`<LINK TO="/PATH">` /PATH는 HashRouter의 Route와 일치하게 작성해야함

```js
// Navigation.js

import React from "react";
import { Link } from "react-router-dom";

function Navigation() {
  return (
    <div>
      <Link to="/">Home</Link>
      <Link to="/about">About</Link>
    </div>
  );
}

export default Navigation;
```

# props

모든 라우터는 default로 props 객체를 가짐

```js
function About(props) {
  console.log(props);
}
```
