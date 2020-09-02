# 'new' 연산자와 생성자 함수

## 생성자 함수
생성자 함수(constructor function)와 일반함수에 기술적인 차이 없음. 생성자 함수는 두 관례를 따름 
- 함수 이름의 첫글자는 반드시 대문자
- 반드시 "new" 연산자를 붙여 실행

**new User(...)를 사용해 함수를 실행하면 동작하는 알고리즘**
- 빈 객체를 만들어 'this'에 할당
- 함수 본문 실행. 'this'에 새로운 프로퍼티를 추가해 'this'를 수정
- 'this'를 반환
```
function User(name) {
  // this = {}; (빈 객체가 암시적으로 만들어짐)
  
  // 새로운 프로퍼티를 this에 추가함 
  this.name = name;
  this.isAdmin = false;
  
  // return this;(this가 암시적으로 반환됨)
  
  let user = new User("Jack"); // name = jack. 아래 코드와 동일하게 동작함.
  
  let user = {
    name: "Jack",
    isAdmin: false
  }
}
```
생성자의 의의는 **재사용 할 수 있는 객체 생성 코드**를 구현하는 것.

> 재사용 할 필요가 없는 복잡한 객체를 만들 때
```
let user = new function() {
  this.name = "John";
  this.isAdmin = false;

  // 사용자 객체를 만들기 위한 여러 코드.
  // 지역 변수, 복잡한 로직, 구문 등의
  // 다양한 코드가 여기에 들어갑니다.
};
```
위 생성자 함수는 익명함수이기 떄문에 어디에도 저장되지 않음. 익명 생성자 함수를 이용하면 재사용 막으며 코드 캡슐화 가능.



