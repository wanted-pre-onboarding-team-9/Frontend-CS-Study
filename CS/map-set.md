# Map과 Set

## Map

- Map은 **키와 값의 쌍**을 가지는 데이터의 모음입니다.
- 키는 고유한 값이어야 하지만, 값은 고유하지 않아도 됩니다.
- 키를 사용하여 값을 검색할 수 있습니다.
- 순서를 보장하지 않습니다.

## Set

- Set은 **고유한 값**을 저장하는 자료구조입니다.
- Set의 값은 중복을 허용하지 않습니다.
- 순서를 보장하지 않습니다.

Map과 Set은 JAVA나 Python 등 여러 언어에서 사용되고, 구현체도 언어마다 상이합니다. 예를 들어 Python에서는 `dict`를 사용하여 Map을 구현하고([Python dictionary](https://wikidocs.net/16043)), JAVA에서는 `HashMap`, `TreeMap`, `LinkedHashMap` 등을 제공하며, `LinkedHashMap`의 경우 순서를 보장한다는 특징을 가지기도 합니다.([JAVA Map](https://wikidocs.net/208))

이번에는 자바스크립트의 Map과 Set에 대해 알아보겠습니다.

<br/>

# Map

- 자바스크립트의 Map은 객체와 비슷합니다.

## 객체와의 차이점

- **Map**은 객체와 달리 객체나 함수를 포함하여 어떤 값이든 키로 사용할 수 있습니다. 반면 **객체**는 문자열 혹은 심볼 타입만 키로 사용 가능합니다.
- `size` 프로퍼티를 사용하여 간단하게 크기를 구할 수 있습니다.
- `forEach`, `for...of` 등의 메서드를 사용할 수 있습니다.

## Map의 메서드와 프로퍼티

**new Map()**

새로운 Map 객체를 생성합니다.

```
const map = new Map()
```

**map.set(key, value)**

키를 이용해 값을 저장합니다. Map 객체를 반환합니다.

```
const str = 'abc'
const obj = {}
const func = function() {}

map.set(str, 'string')
map.set(obj,'object')
map.set(func,'function')
// Map(3) {'abc' => 'string', {…} => 'object', ƒ => 'function'}
```

**map.size**  
요소의 개수를 반환합니다.

```
map.size // 3
```

**map.get(key)**

주어진 키에 해당하는 값을 반환합니다. 값이 없다면 `undefined`를 반환합니다.

```
map.get(str) //'string'
map.get(obj) //'object'
map.get(func) //'function'

map.get('abc') //'string', str === 'string'
map.get({}) // undefined, obj !== {}
map.get(function() {}) //undefined, func !== function() {}
```

**map.has(key)**

키가 존재하면 `true`를, 존재하지 않으면 `false`를 반환합니다.

```
map.has(str) //true
```

**map.delete**

키에 해당하는 값을 삭제합니다.  
해당 요소가 존재할 경우 삭제 후 `true`를 반환하고, 존재하지 않는 경우 `false`를 반환합니다.

```
const wrongStr = 'bb'
map.has(wrongStr) //false

map.delete(str) //true
map.delete(wrongStr) //false

map.has(str) //false
```

**map.clear()**

맵의 모든 요소를 제거합니다.

```
map.clear()
map // Map(0) {size: 0}
```

## Map을 사용할 때 주의할 점

**키 값이 객체일 때는 먼저 변수에 저장한 후에 사용해야 합니다.**

```
const m = new Map()
m.set({ a :'a'}, 'abc')
m.get({ a :'a'}) // undefined

const obj = { b :'b'}
m.set(obj, 'abc')
m.get(obj) // 'abc'
```

- 객체를 키 값으로 그대로 사용할 경우 참조값이 다르기 때문에 `undefined`가 나오게 됩니다.

```
const person1 = { name : 'Jack'}
const person2 = { name : 'Jack'}
console.log(person1 === person2) // false
console.log(person1.name === person2.name) // true
```

- 객체는 평가될 때마다 객체를 생성하기 때문에 `person1`과 `person2`는 별개의 객체입니다.

**데이터를 저장할 때는 set(key,value) 메서드를 사용해야 합니다.**

- 객체처럼 속성을 설정하는 방법은 Map의 데이터 구조와 상호작용하지 않습니다.

```
const m = new Map()

m['a'] = 'a'

console.log(m) //Map(0) {a: 'a', size: 0}

console.log(m.has('a')) // false
```

- 위의 예제와 같이 속성을 설정한 경우 Map의 프로퍼티와 메서드를 사용할 수 없습니다.

## Map 순회하기

### for...of로 순회하기

```
const colorMap = new Map()
colorMap.set(0, 'white')
colorMap.set(1,'black')

for(const [key,value] of colorMap) {
  console.log(`${key} = ${value}`)
}

// 0 = white
// 1 = black
```

- `map.keys()`, `map.values()`, `map.entries()` 메서드를 이용하여 키, 값, 혹은 \[키, 값\] 쌍을 순회할 수 있습니다.

```
// 키 순회
for(let color of colorMap.keys()) {
  console.log(color) // 0, 1
}

// 값 순회
for(let color of colorMap.values()) {
  console.log(color) // white, black
}

// [키, 값] 순회
for(let color of colorMap.entries()) {
  console.log(color) //  [0, 'white'],  [1, 'black']
}
```

### forEach로 순회하기

```
colorMap.forEach((value,key) => {
  console.log(`${key} = ${value}`);
})
// 0 = white
// 1 = black
```

> [Map.prototype.forEach()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map/forEach)

## 객체 -> Map(Object.entries)

- 객체를 Map 객체로 바꾸고 싶을 때는 `Object.entries(obj)`를 사용합니다.

```
const obj = {name:'jack',class:'A'}

const map = new Map(Object.entries(obj))

console.log(map) //Map(2) {'name' => 'jack', 'class' => 'A'}
console.log(map.get('name')) // jack
```

> [Object.entries()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)

## Map -> 객체(Object.fromEntries)

- 반대로 Map을 객체로 바꿀 때는 `Object.fromEntries()`를 사용합니다.

```
const map = new Map()
map.set('0','white')
map.set('1','black')
map.set('2','grey')

let obj = Object.fromEntries(map.entries())

// entries()는 생략 가능합니다.
let obj2 = Object.fromEntries(map)

console.log(obj) //{0: 'white', 1: 'black', 2: 'grey'}
```

# Set

- 자바스크립트의 set은 배열과 비슷합니다.
- 중복을 허용하지 않기 때문에 중복 값을 기록하고 싶지 않을 때나, 배열에서 중복을 제거하고 싶을 때 사용하면 좋습니다.

## Set의 주요 메서드와 프로퍼티

**new Set()**  
새로운 Set 객체를 생성합니다.

```
const set = new Set()
```

**set.add(value)**  
값을 추가하고 Set을 반환합니다.

```
const jack = {name:'Jack'}
const rin = {name: 'Rin'}
const may = {name : 'May'}
set.add(jack) // Set(1) {{…}}
set.add(rin) // Set(2) {{…}, {…}}
set.add(jack) // Set(2) {{…}, {…}} -> 중복되므로 저장되지 않습니다.
```

**set.size**  
요소의 개수를 반환합니다.

```
set.size //2
```

**set.delete(value)**  
해당 요소가 존재할 경우 삭제 후 `true`를 반환하고, 존재하지 않는 경우 `false`를 반환합니다.

```
set.delete(jack) //true
set.delete(may) //false
```

**set.has(value)**  
Set 내에 값이 존재하면 `true`, 없으면 `false`를 반환합니다.

```
set.has(jack) // false(위에서 삭제)
set.has(rin) // true
```

**set.clear()**  
Set의 모든 요소를 제거합니다.

```
set.clear()
set // Set(0) {size: 0}
```

## Set 순회하기

Set은 Map과 마찬가지로 `for...of`와 `forEach`를 이용하여 순회할 수 있습니다.

```
const set = new Set(['white','black','grey'])

for (let value of set) {
  console.log(value)
}

set.forEach((value,valueAgain, set) => {
  console.log(value)
}
```

- `forEach` 콜백의 두 번째 요소는 `value`와 일치합니다. 이는 `Map`과 `Array`에서 사용하는 `forEach`와 동일한 형태를 유지하기 위해서라고 합니다. ([참고](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Set/forEach))

## 배열 -> Set

```
const arr = [1,2,3]

const set = new Set(arr)

set // Set(3) {1, 2, 3}
set.has(1) // true
```

## Set -> 배열

```
const set = new Set()

set.add(1)
set.add(2)

const arr = [...set]
console.log(arr) // [1,2]
```

## 배열에서 Set을 이용하여 중복 제거하기

```
let arr = [1,1,2,3,4,4,5]
const set = new Set(arr)

console.log(set) // Set(5) {1, 2, 3, 4, 5}

// 배열로 되돌리기
arr = [...set] // [1, 2, 3, 4, 5]

// arr -> newArr
let newArr = [...new Set(arr)] // [1, 2, 3, 4, 5]
```

# WeakMap, WeakSet

## WeakMap

- WeakMap의 키로 함수, 객체, 다른 WeakMap 등은 사용할 수 있지만, 원시값은 사용할 수 없습니다.

```
const wm = new WeakMap()

const obj = {}
const func = function() {}
const str = 'a'

wm.set(obj,'object') // WeakMap {{…} => 'object'}
wm.set(func,'function') // WeakMap {ƒ => 'function', {…} => 'object'}
wm.set(str,'string') // Uncaught TypeError: Invalid value used as weak map key
```

- WeakMap의 키로 사용된 객체를 참조하는 것이 없는 경우, 해당 객체는 가비지컬렉팅 대상이 되어 사라집니다.

```
// WeakMap의 경우
let color = {name:'white'}
const weakMap = new WeakMap()
weakMap.set(color, 'abc')
color = null // 객체({name:'white'})를 참조하는 변수가 사라짐 -> 메모리에서 지워집니다.
console.log(weakMap) //WeakMap {}

// Map 객체의 경우
let color2 = {name:'white'}
const map = new Map()
map.set(color2, 'abc')
color2 = null

console.log(map) // Map(1) {{…} => 'abc'}
```

WeakMap은 반복 작업을 할 수 없고, `keys()`, `values()`, `entries()` 메서드를 지원하지 않습니다.

### WeakMap 활용하기

WeakMap은 외부에 속한 객체를 이용하여 부가적인 정보를 추가하고 싶을 때, 혹은 캐싱이 필요할 때 사용할 수 있습니다.

```
const wm = new WeakMap()

let user = {name:'Jack'}

wm.set(user, {visited : true})

console.log(wm.get(user))  //{visited: true}

user = null

console.log(wm.get(user)) //undefined, 유저가 사라지면 방문 정보도 사라지게 됩니다.
```

## WeakSet

WeakSet도 마찬가지로 객체만 저장할 수 있고, `add`, `has`, `delete` 메서드는 사용 가능하지만 `size`, `key()` 등의 메서드는 사용할 수 없습니다.

```
let weakSet = new WeakSet();

let obj1 = { name: 'Jack' };
let obj2 = { name: 'Rin' };

weakSet.add(obj1);

// weakSet에서 객체 존재 확인
console.log(weakSet.has(obj1)); // true
console.log(weakSet.has(obj2)); // false

// 객체 참조 제거
obj1 = null;

console.log(weakSet.has(obj1)); // false
```

> 참고자료  
> [Map - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Map)  
> [Set - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Set)  
> [WeakMap - MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/WeakMap)  
> [맵과 셋](https://ko.javascript.info/map-set)  
> [위크맵과 위크셋](https://ko.javascript.info/weakmap-weakset)  
> [자바스크립트 Map과 Set](https://lakelouise.tistory.com/38)  
> [자바스크립트 Map, Set, WeakMap, WeakSet 간단 설명](https://www.youtube.com/watch?v=8u-ofGrlhQU)
