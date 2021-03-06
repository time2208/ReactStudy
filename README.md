
# React 학습을 목적으로 하고 있습니다.
* 유투부 박성준(https://www.youtube.com/channel/UCPtch39eSiADfztyrTks6pA)의 React 기초를 참고하고 있습니다.

=============
## 내용
* **create-react-app <프로젝트명>**
  * <프로젝트명>으로 React 프로젝트를 생성합니다.

* React에서는 class 대신 className 을 사용한다.
* App 안에서 최상층에는 하나의 부모(테그)만 존재해야 한다.
* 파라미터 (함수)
```javascript
<Person name={"찬"} age={34}></Person>

import React from 'react';
  const Person = (props) => (
     <div>
        <h1>이름: {props.name} 나이는: {props.age}</h1>
     </div>
)

//아래의 형태로 사용 가능
  const Person = ({name, age}) => (
     <div>
        <h1>이름: {name} 나이는: {age}</h1>
     </div>
)

export default Person;
```
* 파라미터 (class)
```javascript
<Person name={"찬"} age={34}></Person>

import React from 'react';

class Person extends React.Componect{
   render(){
      return (
         <div>
            <h1>이름: {this.props.name} 나이는: {this.props.age}</h1>
         </div>
      )
   }
}

//ES6
class Person extends React.Componect{
   render(){
      return (
         const {name, age} = this.props;
         <div>
            <h1>이름: {name} 나이는: {age}</h1>
         </div>
      )
   }
}
export default Person;
```

* state
  * 해당 컴포넌트에서 저장될 자료를 의미한다.
  * class 만이 state를 가질수 있다.
  * 렌더부 변경되어야 하는 경우 state는 갱신을 위한 함수를 별도로 준비해야 한다.
  * state를 갱신시 setState()를 사용한다. 
```javascript
class Person extends React.Componect{
   state = {
      person:[
        {name: "1번", age: 1},
        {name: "2번", age: 2},
        {name: "3번", age: 3},
      ]
   }
   render(){
      return (
         <div>
            <Person name={this.state.person[0].name} age={this.state.person[0].age}</Person>
            <Person name={this.state.person[1].name} age={this.state.person[1].age}</Person>
            <Person name={this.state.person[2].name} age={this.state.person[2].age}</Person>
         </div>
      )
   }
}

//다른 형태
class Person extends React.Componect{
   constructor(props){
      super(props);
      this.state = {
         person:[
           {name: "1번", age: 1},
           {name: "2번", age: 2},
           {name: "3번", age: 3},
         ]
      }
   }
   render(){
      return (
         <div>
            <Person name={this.state.person[0].name} age={this.state.person[0].age}</Person>
            <Person name={this.state.person[1].name} age={this.state.person[1].age}</Person>
            <Person name={this.state.person[2].name} age={this.state.person[2].age}</Person>
         </div>
      )
   }
}
```

* 자식전달
``` javascript
class Person extends React.Componect{
   state = {
      person:[
        {name: "1번", age: 1},
        {name: "2번", age: 2},
        {name: "3번", age: 3},
      ]
   }
   render(){
      return (
         <div>
            <Person name={this.state.person[0].name} age={this.state.person[0].age}
               안녕하세요
            </Person>
         </div>
      )
   }
}

// >
const Person = (props) => (
     <div>
        <h1>이름: {props.name} 나이는: {props.age}</h1>
        <h2>{props.children}</h2>
     </div>
)
//class >
class Person extends React.Component {
   render() {
      const {name, age} = this.props;
      return (
        <div>
           <h1>이름: {props.name} 나이는: {props.age}</h1>
           {this.props.children}
        </div>
      )
   }
}

```

* 함수전달
```javascript
render() {
   const {person} = this.state;
   return(
      <div className="App">
         <Person
           name={person[0].name}
           age={person[0].age}
           myfun={() => console.log("test")}
      </div>
   )
}
//다른형태
render() {
   const {person} = this.state;
   const myfun = () => {console.log("test")};
   return(
      <div className="App">
         <Person
           name={person[0].name}
           age={person[0].age}
           myfun={myfun}
      </div>
   )
}
//Peerson.js
const Person = (pers) =>(
     <h1>이름: {props.name} 나이는: {props.age}</h1>
     <h2>{props.children}</h2>
     {props.myfun()}
)
```
