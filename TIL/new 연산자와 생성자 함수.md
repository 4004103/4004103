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

> 재사용 할 필요가 없는 복잡한 객체를 만들 때.
> 아래 생성자 함수는 익명함수이기 떄문에 어디에도 저장되지 않음. 익명 생성자 함수를 이용하면 재사용 막으며 코드 캡슐화 가능.
```
let user = new function() {
  this.name = "John";
  this.isAdmin = false;

  // 사용자 객체를 만들기 위한 여러 코드.
  // 지역 변수, 복잡한 로직, 구문 등의
  // 다양한 코드가 여기에 들어갑니다.
};
```


## 생성자와 return문
생성자 함수엔 보통 return문이 없음. 반환해야할 것들은 this에 저장되고 자동으로 반환하기 때문.
만약 return문이 있다면
- 객체를 return한다면 this 대신 객체가 반환됨.
- 원시형을 return한다면 return문은 무시됨.
```
// return 뒤에 객체가 오면 생성자 함수는 해당 객체를 반환해주고, 이외의 경우는 this를 반환.
function BigUser() {
  this.name = "John";
  return { name: "Godzilla" }; // <- 객체를 return해서 this가 아닌 새로운 객체를 반환함
}

alert(new BigUser().name); //Godzilla
```

```
// 아무것도 return하지 않음
function SmallUser(){
  this.name = "John";
  return; // <- this를 반환함
}

alert(new SmallUser().name); //John
```

## 생성자 내 메서드
생성자 함수를 사용하면 매개변수를 이용해 객체 내부를 자유롭게 구성 가능.
프로퍼티뿐만 아니라 메서드도 더할 수 있음.
```
function User(name) {
  this.name = name;
  this.sayHi = function() {
    alert("My name is " + this.name);
  };
}

let john = new User("John");

john.sayHi(); // My name is Jhon

/*
john = {
  name: "jhon",
  sayHi: function() {...}
}
*/
```


# 요약
- 생성자 함수(짧게 줄여 생성자)는 일반함수이다. 다만 일반함수와 구분하기 위해 첫글자를 대문자로 씀.
- 생성자 함수는 반드시 new 연산자와 함께 호출돼야 함. new와 함께 호출하면 내부에서 this가 암시적으로 만들어지고, 마지막엔 this가 반환됨.
- 유사한 객체를 여러 개 만들 때 생성자 함수가 유용함.
