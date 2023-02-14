# 0. 목차
```md
0-1. 폴더 리셋하기
0-2. 코드 실행하기

# 변수와 상수
1-0. 변수선언 방법
1-1. 여러가지 타입들
1-2. 상수?

# 조건문
2-0. bool타입이 뭐임?
2-1. if문 사용법
2-2. match표현식 사용법

# 그냥 있는거
3. 코드를 짧게!

# 반복문
4-0. loop문
4-1. while문
4-2. for문

# 메서드
5-0. String의 메서드
5-1. Split<T>관련 메서드

6-0. 정수형 메서드

# 함수형 프로그래밍
7-1. 함수는 쉽죠?
7-2. 소유권
7-3. 익명함수..?

(추가 예정)

# 함수형 프로그래밍
7-2. json같은 struct!
7-3. class외 같은 impl!
7-4. for로 상속을
7-5. 오버라이드로 연산자 가지고 놀기
7-?. 파일을 나눠 코드관리
```

## 0-1. 폴더 리셋하기
자신이 코드를 저장할 폴더를 만든다.
그후 cmd또는 shell을 폴더 경로로 킨다
```
경로가 입력되있는곳에 cmd를 치거나 VScode를 사용중이라면 터미널을 연다
```
이제 `$cargo init`을 입력해보자.
아마 여러 폴더와 파일이 생겼을것이다. 우리는 `src/main.rs`파일에서 코드를 짤것이다.

## 0-2. 코드 실행하기
코드를 실행하는법은 간단하다.
아까 열었던 cmd나 shell에서 `$cargo run`을 입력한다. 그러면 `src/main.rs`파일이 실행될것이다.


## 1-0. 변수선언방법
```rs
let 변수명: 타입 = 값
```
이런식으로 변수를 생성할수있다.
`변수명`에는 말그대로 변수명이 들어간다. `: 타입`부분은 **타입 어노테이션**이라고 부르며 굳이 쓰지않아도 된다. `값`부분에도 말그대로 값이 들어간다.

### 1-0.5. 변수 출력하기
`println!`또는 `print!`메크로를 사용하여 출력할수있다.
메크로는 일단 끝에 !가붙은 특별한 함수라고 생각하고 넘어가고 나중에 배워보자.
```rs
fn main(){
    let 변수: i32 = 1;
    println!("{} {}", 변수, 변수 + 1); // 방법1
    println!("{변수}"); //  방법2
}
/*
출력값:
1 2
1
*/
```
이런식으로 포멧을 하여 출력할수 있다.
`방법1`은 변수의 값을 {}와 치환(?)하여 출력한다.
`방법2`는 순수한 변수만 사용할수있는 방법이다. 순수한 변수는 `변수.메서드()` `변수.0`같은게 아닌 오직 `변수`만 있는것을 말한다

## 1-1. 여러가지 타입들
rust에는 많은 타입이있다. 우리는 가장 기초적인(?) 타입을 알아볼것이다.

### 1-1-1. 정수
먼저 `정수(integer)`타입을 알아보자.
정수는 2가지 종료가 있다.
부호가 들어가는 타입(signed type): `i8` `i16` `i32` `i64` `i128` `isize`
부호가 들어가지않는 타입(unsigned type): `u8` `u16` `u32` `u64` `u128` `usize`
`i`또는 `u`뒤에 들어가는 숫자는 몇bit를 저장할수있는 변수인지 알려준다.
변수의 최대치는 `정수형::MAX` 변수의 최소치는 `정수형::MIN`으로 알수있다.

범위공식: `-2^(bit) ~ 2^(bit)+1`
\*참고 usize, isize는 자신이 설치한 rust컴파일러의 bit이며 u32또는 u64의 값을 갖게 된다.

### 1-1-2. 문자열
문자열은 두가지 타입이있다.
`&str`타입과 `String`타입이다.
먼저 `&str`타입에 대하여 알아보자.
```rs
fn main(){
    let s: &str = "문자열";
}
```
위 코드처럼 변수에 값을 넣을수있다.
다음으로는 `String`타입에 대하여알아보자.
`String`타입의 기본값은 `String::new()`이며 자신이 원하는문자열을 저장하고싶다면 `String::from(&str)`을 사용할수 있다.
```rs
fn main(){
    // 기본값 String문자열
    let s1: String = String::new();

    // 원하는 문자열
   let s2: String = String::from("내가 원하는 문자열임");
}
```
이렇게 쓸수있다.

### 1-1-3. 배열
배열은 여러가지 타입이 있지만 가장 많이쓰는 2가지를 알아보자.
먼저 `[T; usize]`T자리에는 자신이 배열에 넣고싶은 타입을 쓰면되고 usize자리에는 usize타입의 정수를 넣어주면 된다.
```rs
//예시
fn main(){
    let arr_int: [i32; 3] = [0, 2, 5];
    let arr_str: [&str; 4] = ["5", "-", "2", "3"];
}
```
다음으로는 `Vec(Vector)`베열에 대하여 알아보자.
`Vec<T>`타입은 위에 있는 배열과는 다르게 크기가 자유로운편이다. 그래서 크기를 쓰지 않아도 된다. T자리에는 자신이 저장할 타입을 써주면되며 `vec![]`메크로를 사용하여 값을 저장하고 `.push`메서드를 사용하여 값을 추가할수 있다.
```rs
//예시
fn main(){
    let mut arr: Vec<i32> = vec![2, -1, 7]; //여기 사용되는 mut키워드는 다음에 나오는것을 참고하기 바란다.
    arr.push(10); // 이렇게하면 arr의 값이 vec![2, -1, 7, 10] 이 된다.
}
```

\*참고: 만약 arr(배열)을 출력하려면 `println!("{:?}", arr)` `println!("{:#?}", arr)` `println!("{arr:?}")` `println!("{arr:#?}")` 등의 방식으로 출력할수있다.

### 1-1-4. mut키워드가 뭐야?
mut(mutable)키워드는 변수의 값을 바꿀수있게 해주는 키워드다.
```rs
//실행되지 않습니다!!
fn main(){
    let a: i32 = 1;
    a = 2;
}
```
위와같은 코드가 작동하지 않아서 당황했던적이 있을것이다.
그럴땐 mut키워드를 써보자.
```rs
// 이렇기쓰면 오류안남
fn main(){
    let a: i32 = 1;
    let a = 2;
}
```
사용법은 변수를 선언할때 mut키워드흫 붙여주는것이며 아레 예시처럼 쓴다.
```rs
let mut 변수명: 타입 = 값
```
이렇게 mut키워드를 붙이면 변수를 다시 선언하지 않고도 변수의 값을 바꿀수 있다.
```rs
//예시
fn main(){
    let mut a: i32 = 1;
    a = 2; //여기서 변수의값이 변경되기때문에 mut키워드를 써줘야한다.

    let mut arr: Vec<i32> = vec![2, -1, 7];
    arr.push(10); //여기서 변수의값이 변경되기때문에 mut키워드를 써줘야한다.
}
```

## 1-2. 상수?
상수는 값을 변경할수 없는 변수이다.
만드는 방법은 let이 아닌 const를 써주면 된다.
```
fn main(){
    const ASDF: i32 = 10;
}
```
`*참고` 상수의 이름은 모두 대문자로 써줘야하는 암묵적약속이 있으며 상수에는 mut키워드를 당연하게 사용할수없다.

## 2-0. bool타입이 뭐임?
bool타입은 `true`와 `false`밖에 없다.
다른언어에서는 0은 false 0이 아닌것은 true로 보지만 rust는 그렇지 않으니 중 해야한다.

## 2-1. if문 사용법
if문은 `if bool{}`로 쓰며 bool이 true일 경우에 {}에 있는 코드를 출력한다.
bool은 자리에는 여러가지 표현식(?)이 들어갈수있다.
a와 b변수가 있다면
```rs
a == b  // a와 b가 같다.
a != b  // a와 b가 같지않다.
a > b   // a가 b보다 크다.
a >= b  // a가 b보다 크거나 같다.
a < b   // a가 b보다 작다.
a <= b  // a가 b보다 작거나 같다.
```

## 2-2. match문 사용법
match식은 아레와 같이 사용할수 있다.
```rs
match 변수{
    표현식 => { /* 1번 */ }
    _ => { /* 2번 */ }
}
```
변수가  패턴이 같다면 1번 코드가 아니라면 2번 코드가 실행된다.
표현식은 여러가지가 있다
그냥 값을 적는다면 그값과 같을경우 실행한다.
`a..=b`를 적는다면 a~b a이상 b미만일 경우 실행한다. a와 b는 정수형타입 이거나 char타입이다.
`a | b`를 적는다면 a또는 b일때 실행한다.
```rs
// 예시(변수 a를 바꾸면서 해보면 쉽게 알수있을것이다.)
fn main(){
    let a: usize = 10;
    match a{
        0..=5 => println!("0~5임!"),
        6 | 7 => println!("6이야 7이야?"),
        x => println!("{}", format!("당연히 {x}야!")) // fotmat 메크로는 print메크로에 있던 문자열 포멧을 할수있게 해주는 메크로이며 String타입을 반환한다.
    };
}
```

## 3. 코드를 짧게!
코드 길이를 단축시키는걸 해보자.
변수 여러개를 만든다면
```rs
let (a, b): (i32, &str) = (10, "!!")
```
코드를 이런식으로 줄일수 있다.

만약 길이가 긴 배열을 만들어야한다면 값으로 `[a; b]`를 넣어보자. a를 b길이만큼 채워넣는다.
예시로
```rs
fn main(){
    let a: [i32; 5] = [0; 5];
    println!("{a:?}");
}
```
이러면 `[0, 0, 0, 0, 0]`가 출력된다
Vec<T>타입도 마찮가지로 vec![a; b]를 쓸수 있다.

조건식과 관련된 변수를 만들어야한다면`return`을 이용해보자
```rs
fn main(){
    let a: bool = true;
    let b = if a{return 1;}else {return 0;}
}
```
위 코드처럼 쓰면 a가 true일때 b는 1 아닐때는 0을 갖게 만들수 있다.
하지만 저것도 길어보이니 `return`을 생략해보자.
rust에서는 값뒤에 `;`이 없다면 return값으로 인식한다.
```rs
fn main(){
    let a: bool = true;
    let b = if a{1}else {0}
}
```
그러니 이렇게 위 코드처럼 줄일수 있다.

## 4-0. loop문
loop문은 코드를 무한이 반복하고싶을때 사용한다.
사용방법은 간단하다 `loop {}`
{}안에 있는 코드가 계속 반복되며 break를 만나면 멈춘다.
```rs
// "도배"가 무한이 출력되는 코드
fn main(){
    loop{
        println!("도배");
    } 
}
```

## 4-1. while문
while문은 조건이 맞다면 계속 반복한다
사용방법은 아레 코드와 같다
```rs
while bool{}
```
bool값이 true이면 {}안에 코드를 반복한다 bool값이 false가 되거나 break를 만나면 멈추게된다.
```rs
// 0 ~ 5가 출력되는 코드
fn main(){
    let mut a = 0;
    while a <= 5{
        println!("{a}");
        a += 1;
    }
}
```

## 4-2. for문
for문은 `for range`와 `for each`로 두가지가 있다.

### 4-2-1. for range
for range는
```rs
for i: t in a..b{}
```
처럼 코드를 쓴다. a부터 b-1의 값이 하나씩 i에 들어가지며 반복된다.
t에는 정수형 타입이나 &str이 들어갈수 있다. break를 만나거나 i의 값이 b-1과 같아지면 멈춘다
```rs
// 0 ~ 5를 출력하는 코드
fn main(){
    for i in 0..6{
        println!("{i}");
    }
}
```
### 4-2-2. for each
for each는
```rs
for i: t in arr{}
```
arr에는 배열을 쓰고 t는 배열안에 아이템의 타입을 쓴다.
arr의 마지막 값과 i의 값이 같거나 break를 만나면 멈춘다.
```rs
// 0 ~ 5를 출력하는 코드
fn main(){
    let arr: [usize; 6] = [0, 1, 2, 3, 4, 5];
    for i: usize in arr{
        println!("{i}");
    }
}
```

## 5-0. String의 메서드
String의 메서드를 알아보도록 하자.
### 5-0-1. new
new 메서드는 String 구현채의 생성자(constructer)이다.
```rs
String::new()
```
이런식으로 사용할수 있으며 기본값을 가진다

### 5-0-1. from
from 메서드는 String 구현채의 또 다른 생성자(constructer)이다.
```rs
String::from("입력")
```
`&str`타입을 인수로 받고 그 값을 가진다.

### 5-0-2. replace
a문자를 b문자로 변경해야할때 사용되며 String타입을 반환한다.
```rs
let s = String::from("fuck you");
```
이런 String이 있다고 해보자. 이때 fuck love로 변경하려면 아레 코드를 쓰면된다.
```rs
let mut s = String::from("fuck you");
s = s.replace("fuck", "love");
```

### 5-0-3. as_str
가끔 String을 &str로 변경해야하는 상황이 생길것이다. 이때 as_str메서드를 사용하면된다.
```rs
let s = String::from("String");
let s_2 = s.as_str();
```

### 5-0-4. trim
뜻 그대로 String을 다듬는 메서드이다.
이 메서드는 문자열 시작/끝에있는 `\t` `\n` `\r` ` `와 같은 문자를 지워준다.
```rs
let s = String::from("  \tString\r\n");
let s_2 = s.trim();
```

### 5-0-5. split
문자열을 자를때 사용된다.
예를들어서 `a s d f`라는 문자 가 있을때 ` `문자를 기준으로 자르려면 아레 코드를 쓰면 되며 `Split<&str>`타입이 반환된다.
```rs
let s = String::from("a s d f");
let arr = s.split(" ");
```

## 5-1. Split<T>관련 메서드
문자열을 나누면 Split<T>와 비슷하거나 같은 구현체가 반환된다.


### 5-1-1. collect<T>
T타입으로 변환해주는 메서드다
`<T>`는 제네릭 타입이라고하고 함수에서는 `함수::<T>()`형태로 사용할수 있다.
```rs
let binding = String::from("a s d f");
let s = binding.split(" ");
let v = s.collect::<Vec<&str>>(); // 변환된거
```
이런식으로 `Split<&str>`타입으로 `Vec<&str>`타입으로 변환해줄수 있다.

### 5-1-2. map
\*\* 이거는 나중에 배울 익명함수가 사용되는 메서드다.
Split<T>의 값을 조금식 바꿔서 저장해주는 메서드 이며 Split<T>타입을 반환한다
```rs
let binding = String::from("1 2 3 4");
let s = binding.split(" ");
let v = s.map(|x|x.parse::<usize>().unwrap());
```
이런식으로 값을 usize타입으로 바꿔줄수 있다.

**6-0. 정수형 메서드**
__`6-0-1. abs`__
절댓값(ABSolute value)을 구하는 메서드이다
```rs
let mut a = -10;
a = i32::abs(a);
```
이러면 a의 값이 10이된다

### 6-0-2. pow
제곱을 구하는 메서드이다
```rs
i32::pow(10, 2)
```
이런식으로쓰면 10의제곱(100)이된다.

### 6-0-2. from_str_radix
n진법이 주어젔을때 그걸 10진법으로 변환하는 코드이다.
```rs
let mut a = i32::from_str_radix("100", 2).unwrap();
```
이런식으로 쓸수 있으며 2진법 100은 10진법으로 4이기때문에 a의값은 4가된다.

## 7-1. 함수는 쉽죠?
```rs
fn 이름(파라미터: 파라미터_타입) -> 반환타입{
  코드;
  반환값
}
```
이런식으로 쓸수있다.
아레는 덧셈 함수의 예시이다.
```rs
fn sum(a: i32, b: i32) -> i32{
  a + b // a + b의 값이 반환됨
}
```
이러면 a+b의값이 반환된다.
### 7-1-1. 주의사항
rust는 반환방식이 2가지가 있다.
`return 값;`을 하는방법과 `값`을 쓰는방법이다
```rs
// 작동 안함
fn sum(a: i32, b: i32) -> i32{
  a + b;
}
```
이러면 a + b뒤에 `;`이 있기때문에  반환값으로 인식을 하지 않기때문에 오류가 난다.

### 7-1-2. 제네릭타입
전에 많이봤듯이 `<T>`를 사용하여 나타넬수 있다.
```rs
fn q<T>(a: T) -> T{
    a
}
```
이런식으로  만들수있다.
만약 두가지 타입을 받고싶다면
```rs
fn q<T, Q>(a: T, b: Q) -> (T, Q){
    (a, b)
}
```
이런식으로 `<>`자리에 여러가지 타입을 쓰면된다.

## 7-2. 소유권
소유권은 rust에서 중요하고 어려운 개념이다.
```rs
// 실행 안됨
fn main(){
    let a = String::from("asdf");
    let b = a;
    print!("{a}")
}
```
이 코드는 실행되지 않는다.
**`소유권`**때문이다. 
~~a의 값이 복사되서 b변수로 가는게 아니라 그냥 전채의 값이 b로 가게된다. 그러면 a의값은 쓸수없게된다.~~
라고 말하면 어려울것같으니 쉽게 이해해보자.
```
나(a)는 asdf라는 물건의 주인이라 해보자. 나(a)는 asdf를 다른사람 (b)에게 팔았다.
이때 나(a)는 asdf를 사용할수 없게된다.
```
이렇게 말하면 조금 쉬울것이다.

\*자세한거는 이 영상을 보면 쉽게 알수있다: <https://youtu.be/w1dlmOjDLX8?t=418>

### 7-2-1.빌려주기
그러면 만약 판매하는게 아니라 빌려주는 방법을 써보자.
빌려주는방법은 참조연산자(&)를 사용하는것이다

```rs
// 참조연산자(&)를 사용하는 방법
let a: String = String::from("asdf");
let b: &String = &a;
println!("{a}");
println!("{b}");
```

### 7-2-2.복사해주기
그러면 만약 판매하는게 아니라 빌려주는 방법을 써보자.
복사해주는방법은 clone메서드를 사용하는것이다
```
// clone메서드를 사용하는 방법
let a: String = String::from("asdf");
let b: String = a.clone();
println!("{a}");
println!("{b}");
```

## 7-3. 익명함수..?
`5-1-2. map`에 한번 나왔었다.
사용방법은 아레와 같다.
```rs
| 파라미터: 파라미터_타입 | -> 반환타입{ 코드; 반환값 }
```

```rs
let a = | a: i32, b: i32 | -> i32{ a + b };
println!("{}", a(1, 2))
```
예시로 이거는 a와 b를 더하는 익명함수다.

### 7-3-1. 함수의 인수로 익명함수 넣기
```rs
fn main(){
    let a = asdf1(10, |x|x + 1);
}

fn asdf1(x: i32, f: impl Fn(i32) -> i32) -> i32 {
    f(x)
}
```
처럼 쓸수있다 `Fn`자리에는 파라미터의 타입이 들어가도 -> 뒤에는 반환값이 쓰여진다.
FnMut FnOnce등도 있는다
