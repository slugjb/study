## React란??
***
 * function Test(){} → function component
 * class Test extends React.Component → class component
 * react는 자동적으로 모든 class component의 render method를 실행하려 함
 * state는 object이고, component의 data를 넣을 공간이 있고 이 데이터는 변한다 → state 정의/추가설명 보충 필요
 * setState를 사용하지 않으면 state값이 변해도 새 state값과 render function이 호출이 안됨
```
  add = () => {
    this.setState(current => ({count: current.count + 1}));
  };  // state를 set 할 때, react에서 외부의 상태에 의존하지 않는 가장 좋은 방법
  minus = () => {
    this.setState({count: this.state.count - 1});
  };  // 좋지 못한 문구 is not awesome
```

*  Mounting- component의 태어남  
    ▶ constructor()-JS에서 class를 만들 때 호출되는 것 - coponent가 mount될 때 호출됨  
    ▶ componentDidMount() - component가 처음 render될 때 호출됨

    ※ Updating
     ▶ componentDidUpdate()-coponet가 업데이트될 때 호출됨

    ※ Unmounting- coponent가 죽는 것
     ▶ componentWillUnmount()

   setState()호출 => component 호출 => render 호출 => 업데이트 완료 후 coponentDidUpdate 실행

   * setState사용 할 때 state안에 default 값을 미리 선언 할 필요는 없다  

## 09.17
 원하는 모든 component에 대한 css 파일을 만들 수 있고, 하나의 css 파일에 모든 것을 넣을 수도 있다. put every thing


  1. npm i gh-pages / gh-pages는 너의 웹사이트를 github의 page 도메인에 나타나게 해줌(Html, Css, Javascript)  


  2. git remote -v / 경로 확인 /  일반적인 동작 방식은 github에서 너의 project 이름을 get 한다.  
    ex) https://slugjb.github.io/movie_app_09/      // username + github.io/프로젝트명/ 
    

  3. gh-pages / github에 업로드 하는것을 허가해 주는 모듈 설치


  4. package.JSON에 주소 추가 / ` "homepage": "https://slugjb.github.io/movie_app_09/" `
        
        * 이 단계는 필수, 정말로 진짜로, gh-pages가 동작하는데 필수!!  
           ※주의 : 꼭 '소문자'여야 함. / github에 있는 프로젝트 명 / every thing lower case
           
  5. npm run build / 명령어를 통해 build 폴더를 생성하고 minimaze 함  
       gh-page를 호출하고 folder를 upload해야하는데 folder가 없어서 생성
         
         
  6.  package.JSON 내의 "scripts" 부분에 "deploy": "gh-pages -d build", "predeply": "npm run build" 추가!!  
     deploy를 호출할경우 npm은 super smart하기 때문에 predeploy를 먼저 호출하고 build는 build script를 호출함  
     그리고 그 script는 folder를 준다. 이것이 완료되면 predeploy는 끝난다.  
     Terminal에 npm run build를 입력해 성공적으로 완료되면 publish 문구를 볼 수 있다.

***
## react-router-dom란?
 react에서 네비게이션을 만들어 주는 패키지 / 참조 npmjx.com/package/react-router-dom  
라우터는 rul을 가져다가 확인하고, 우리가 명령한 컴포넌트를 불러온다  
라우터를 만들고 그 다음 라우터에는 스크린을 넣음, 그래서 원하는 만큼 path를 만들 수 있음  
라우터 안에는 매우 중요한 props가 한개 들어감, 그 props는 렌더링할 스크린이 들어가고 다른 prop이 뭐 할지 정해줌


```
<HashRouter>
   <Route path="/" component={Home} />
   <Route path="/about" component={About} />
</HashRouter>
```
  이런 형태의 라우터 일경우에 http://localhost:3000/#/about 이러한 url 이면,  
  먼저 Home의 Component를 rendering 하고, 후에 /about의 경로의 About Component를 rendering한다.  
  이를 방지하기 위해 exact 를 사용한다.
```
<HashRouter>
   <Route path="/" exact={true} component={Home} />
   <Route path="/about" component={About} />
</HashRouter>
```
   사용시 거쳐가는 경로가 아니라 정확한 경로의 Component만 rendering한다.
***
  Navi 사용
```
<div>
   <a href="/">Home</a>
   <a href="/about">About</a>
/div>
```
  처음 경로, 즉 home으로는 이동이 가능하지만 /about은 작동하지 않는다. 왜일까?   
  왜냐하면 href는 html이기 때문. html은 (전체_페이지를 새로고침 하기 때문이다.  
  즉, react가 죽고, all page가 refresh되어버리기 때문, react로 만든 페이지이고
  interaction을 원하지만, 이러한 방식은 원하지 않는다.
```
<div>
   <Link to="/">Home</Link>
   <Link to="/about">About</Link>
</div>
```
    위와 같은 방식을 사용
***
  Route는 Route안에서만 사용하는것이 좋다. 밖에서는 사용 불가  
 HashRouter와BrowserRouter 의 차이점은 거의 없지만,  
 Hash는 주소창에 http://localhost:3000/#/  처럼 #이 나오고,  
 BrowserRouter은 http://localhost:3000 이렇게 url이 나온다.
 
 이 외에는 BrowserRouter가 github pages에 정확히 설정하기가 불편하다. Hash가 쉽다.
    
***
## 깃허브에 페이지 배포하기
  1) npm i gh-pages
  2) package.json에 homepage 추가하기
  3) scripts에 ▷ "deploy" : "gh-pages -d build" ▷   
       "predeploy" : "npm run build"→deploy를 호출하면 먼저 호출된다
 4) npm run deploy Published

   https://slugjb.github.io/movie_app_09/#/  ← 위의 방법을 통해 구현한 웹 / React를 이용, API에서 DATA GET
     
***
  ##  Error

   page not found - 서버가 없어서 못 찾는것.

   항상 Npm Start 실행 후 그대로 둘 것.

   localhost를 계속 유지하고 refresh 하기 위하여 npm start 실행

   Each child in a list should have a unique “key” prop.

   모든 react의 element는 유일해야하고, 이런 처리 없이 데이터를 넣으면 list에 넣을때 유일성을 잃는다.  
   그래서 각각의 item에 id값을 준다.

   `정리 필요`

***

  정의
 
## React란?
  페이스북에서 개발한 UI Library (재사용 가능한 UI를 생성 가능하게 한다)
  
## Virtual Document Object Model
  UI의 이상적인 또는 가상적인 표현을 메모리에 저장하고 ReactDOM과  
  같은 라이브러리에 의해 실제 DOM과 동기화하는 프로그래밍 개념

## JSX
  javascript + xml / javascript 안의 html / React에서 나온 특화된 개념

## Component
   UI를 구성하는 개별적인 뷰단위,생산성이 높고, 유지보수 용이
***
> 보통의 Web은 index.html을 호출하는데, 호출시에 React는 처음부터  
> Html에 넣지 않고 Html에서 Html을 추가하거나 제거가 가능하다.
>
> Empty Html을 호출하고 React가 Component에 작성한 Html을 Push해준다.  
> 그래서 화면 구현시 Sources 부분에 코드가 나오지 않는다.
> 
> React는 Component와 함께 동작, Component는 Html을 Return한다.
> 
> App.js에서 함수 정의하고, Index.js에서 호출명을 정의하고, 정의한 호출명을 Index.html에서 사용한다.
> 
> Component 작성 때마다 import react 'react'; 선언  // var React = require('react'); 와 동일하다.  
> 미 선언시 react가 jsx가 있는 component를 사용하는 것을 이해하지 못한다.
> 
> React는 Component를 가져와 Brower가 이해할수 있는 평범한 Html로 구성해준다.
