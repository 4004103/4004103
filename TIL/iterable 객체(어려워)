# iterlable 객체
반복 가능한(iterlabel) 객체는 배열을 일반화한 객체입니다. 이터러블이란 개념을 사용하면 어떤 객체든 `for..of`반복문을 적용할 수 있음.
배열이 아닌 객체가 있는데 이 객체가 어떤 것들의 컬렉션(목록, 집합 등)을 나타내고 있는 경우 `for..of` 문법을 적용하면 컬렉션 순회가 쉬워짐. 이게 가능하도록 해봅쉬당

## Symbol.iterator
`range`를 이터러블로 만들려면 (`for..of`가 동작하도록 하려면) 객체에 `Symbol.iterator`(특수 내장 심볼)라는 메서드를 추가해 아래와 같은 일이 벌어지도록 해야함.
- `for..of`가 시작되자 마자 `for..of`는 `Symbol.iterator`를 호출합니다(`Symbol.iterator`가 없으면 에러 발생). `Symbol.iterator`는 반드시 (iterator, 메서드 `next`가 있는 객체)를 반환해야함.
- 이후 `for..of`는 반환된 객체(이터레이터)만을 대상으로 동작함
- `for..of`에 다음 값이 필요하면 `for..of`는 이터레이터의 `next()`함수를 호출함.
- `next()`의 반환값은 `{done: Boolean, value: any}`와 같은 형태여야 함. `done = true`는 반복이 종료되었음을 의미함. `done = false`일땐 `value`에 다음값이 저장됨.

`range`를 반복 가능한 객체로 만들어주는 코드
```javascript
let range = {
  from: 1,
  to: 5,
}

// 1. for..of 최초 호출 시, Symbol.iterator가 호출됨
range[Symbol.iterator] = function() {
  
  // Symbol.iterator는 이터레이터 객체를 반환함.
  // 2. 이후 for..of는 반환된 이터레이터 객체만들 대상으로 동작하는데, 이때 다음 값도 정해짐.
  return {
    current: this.from,
    last: this.to,
    
    // 3. for..of 반복문에 의해 반복마다 next()가 호출됨.
    next() {
      // 4. next()는 값을 객체 {doen:.., value:..}의 형태로 반환해야 합니다....
      if (this.current <= this.last) {
        return{ done: false, value: this.current++ };
      } else {
        return { doen: true };
      }
    }  
    
  };
};

// 이제 의도한 대로 동작합니다...
for (let num of range) {
  alert(num) // 1, then 2, 3, 4, 5
}
```



