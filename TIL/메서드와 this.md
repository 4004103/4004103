# 메서드와 this
객체의 프로퍼티에 함수를 할당해 행동할 수 있는 능력 부여해줌.

##  메서드 만들기
```
let user = {
  name: "John",
  age: 30,
};

user.sayHi() = function {
  alert("안녕하세요!");
};

user.sayHi(); // 안녕하세요!
```
객체 프로퍼티에 할당된 함수를 메서드(method)라고 부름.
위 예시에선 'user'에 할당된 'sayHi'가 메서드임.

정의된 함수를 메서드로 만들 수도 있음
```
let user = {
  //...
}

// 함수 선언
function sayHi() {
  alert("안녕하세요!");
}

// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;

user.sayHi(); //안녕하세요!
```

## 메서드 단축 구문
객체 리터럴 안에 메서드를 선언할때 사용할 수 있는 단축 문법
```
 // 아래 두 객체는 동일하게 동작함
 
 user = {
  sayHi: function() {
    alert("안녕하세요!");
  }
 };
 
 // 단축구문
 user = {
  sayHi() { // 'sayHi: function()' 과 동일함
    alert("안녕하세요!");
  }
 };
```

## 메서드와 'this'
대부분의 메서드는 객체 프로퍼티의 값을 활용함. 메서드 내부에서 'this'키워드를 사용하면 객체에 접근 할 수 있음.
'점 앞'의 'this'는 객체를 나타냄. 정확히는 메서드를 호출할 때 사용된 객체.
```
let user = {
  name: "John",
  age: 30,
  
  sayHi() {
    // 'this'는 '현재 객체'를 나타냅니다. (user)
    alert( "this.name" );
  }
};

user.sayHi(); // John

// 'this'를 사용하지않고 외부 변수를 참조해 객체에 접근 가능하지만 애러 발생할 수 있음.
let usert = {
  name: "John",
  age: 30,
  
  sayHi() {
    alert(user.name); // Error: cannot read property 'name' of null
  };
};

let admin = user;
user = null; // user를 null로 덮어 씌움

admin.sayHi(); // sayHi()가 엉뚱한 객체를 참조하며 에러발생
```

## 자유로운 'this'
자바스크립트에선 모든 함수에 'this' 사용 가능.
'this'값은 런타임에 의해 결정됨. 컨텍스트에 따라 달라지고 동일한 함수라도 다른 객체에서 호출했다면 'this'가 참조하는 값이 달라짐.
```
 let user = { name: "John" };
 let admin = { name: "admin" };
 
 function sayHi() {
  alert( this.name );
 };
 
 //별개의 객체에서 동일한 함수를 사용함
 user.f = sayHi;
 admin.f = sayHi;
 
 //'this'는 '점(.) 앞의' 객체를 참조하기때문에 this값이 달라짐
 user.f(); // John ( this == user )
 admin.f(); // admin ( this == admin )
 
 admin['f'] // admin (점과 대괄호는 동일하게 동작함!)
 // obh.f() 를 호출하면 this는 f를 호출하는 동안의 obj임.
```

## 'this'가 없는 화살표 함수
화살표 함수는 '고유한 this'를 가지지 않음.
화살표 함수에서 'this'를 참조하면 화살표 함수가 아닌 '평범한 외부함수'에서 'this'값을 가져옴.
```
// 예시의 함수 'arrow()'의 'this'는 외부함수 'user.sayHi()'의 'this'가 됨.
let user = {
  firstName: "보라",
  sayHi() {
    let arrow = () => alert(this.fistName);
    arrow();
  }
};

user.sayHi() // 보라
```


# 요약
- 객체 프로퍼티에 저장된 함수를 '메서드'라고 함
- object.doSomthing()은 객체를 '행동'할 수 있게 해줌
- 메서드는 this로 객체를 참조

this 값은 런타임에 의해 결정됨.
- 함수를 선언할 때 this를 사용할 수 있지만 함수가 호출되기 전까지 this에는 값이 할당되지 않음
- 함수를 복사해 객체 간 전달 가능
- 함수를 객체 프로퍼티에 저장해 object.method() 같이 '메서드'형태로 호출하면 this는 object를 참조함
- 화살표 함수는 자신만의 this를 가지지 않아 화살표 함수 안에서 this를 사용하면 외부 this 값을 가져옴
