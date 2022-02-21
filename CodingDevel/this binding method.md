# this binding method
> <a href="https://github.com/HELLOHIDI/js-study/blob/main/CodingDevel/basic/8.%20this%20%ED%82%A4%EC%9B%8C%EB%93%9C.md">'this'는 호출에 따라 어디에 바인딩 되는지 달라진다.</a><br>
> but. 호출에 상관없이 **명시적으로 this를 지정**하게 하는 메소드들이 있다.

## call(this로 사용될 값, ...함수가 사용할 매개변수)
> **this를 특정값으로 지정 가능한 메소드**
> **모든 함수**에서 사용 가능하다.

```javascript
const mike = {
  name : "Mike",
};

const tom = {
  name : "Tom",
};

function showThisName() {
  console.log(this.name);
}

showThisName(); // Window -> 여기서 this는 window를 가리킴
showThisName.call(mike); // this를 사용할 객체를 mike를 설정했기 때문!

function update(birthYear, occupation){
  this.birthYear = birthYear;
  this.occupation = occupation;
};

update.call(mike,1999, 'singer'); //call(this로 사용될 값, ...함수가 사용할 매개변수)
console.log(mike);

// {name : "Mike", "birthYear" : 1999, "occupation" : "singer"}
```


## apply
> **call과 완전히 same but. 매개변수를 배열로 받는 메소드**
> 
```javascript
const tom = {
  name : "Tom",
};

function update(birthYear, occupation){
  this.birthYear = birthYear;
  this.occupation = occupation;
};

update.apply(tom, [2000, 'teacher']);
```

## bind
> **함수의 this값을 영구히 바꿀 수 있는 메소드**

```javascript
const mike = {
  name : "Mike",
};

function update(birthYear, occupation){
  this.birthYear = birthYear;
  this.occupation = occupation;
};

const updateMike = update.bind(mike); // 항상 mike를 this로 가짐
updateMike(1980, "police");
console.log(mike); //{name : "Mike", "birthYear" : 1980, "occupation" : "police"}


```


#### 예시 코드
```javascript
const user = {
  name : "Mike",
  showName: function () {
    console.log(`hello, ${this.name}`);
  },
};

user.showName(); // "hello, Mike"

let fn = user.showName;
fn(); // "hello," => this를 잃어버림

fn.calll(user); // "hello, Mike"
fn.apply(user); // "hello, Mike"

let boundFn = fn.bind(user);
boundFn(); // "hello, Mike"
```
