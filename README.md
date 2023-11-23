# Dart
## 변수
``` dart
void main() {

  // var는 타입을 재할당이 불가능하다.
  var name = 'var test';
  print(name); // 출력 var test;

  name = 123; // 에러 발생

  // dynamic은 타입을 재할당 할 수 있다.
  dynamic name2 = 'var test';
  print(name2); // 출력 var test;

  name2 = 123; // name에 123 입력
  print(name2); // 123
}
```

## nullable, non-nullable
``` dart
void main() {

  // nullable - null이 될 수 있다.
  // non-nullable - null이 될 수 없다.
  
  // dart의 기본 변수는 null이 들어갈 수 없다.
  String name = "aa";
  name = null; // 에러 발생
  
  // 타입에 ?를 명시해주면 null을 넣을 수 있다.
  String? name2 = "aa";
  name2 = null; // 성공
}
```

## final과 const
``` dart
void main() {

  // const는 빌드 타임에 값을 몰라도 된다.
  final DateTime now = DateTime.now(); 
  
  // const는 빌드 타임에 값을 알고 있어야 한다.
  // DateTime.now()은 어떤 값이 들어올지 빌드 타임에는 값을 알지 못하기 때문에 사용이 불가능하다.
  const DateTime now2 = DateTime.now(); 
}

```

## 함수
``` dart
void main() {
  addNumber(10, y: 20);
  
  arrowFunctionVerAddNumber(20, y: 30);

  Operation operation = add;
  int result = operation(10, 20, 30);
  
  operation = subtract;
  int result2 = operation(10, 20, 30);
  
  int result3 = calculate(30, 40, 50, add);
  int result4 = calculate(30, 40, 50, subtract);
  
  print(result);
  print(result2);
  print(result3); 
  print(result4);
  
}

// positional parameter - 순서가 중요한 파라미터
// optional parameter - 있어도 되고 없어도 되는 파라미터
// named parameter - 이름이 있는 파라미터(순서가 중요하지 않다.)

addNumber(
  int x, {
  required int y,
  int z = 30,
}) {
  int sum = x + y + z;
}

// arrow function - 화살표 함수
arrowFunctionVerAddNumber(
  int x, {
  required int y,
  int z = 30,
}) =>
    x + y + z;

// typedef
typedef Operation = int Function(int x, int y, int z);

// 더하기
int add(int x, int y, int z) => x + y + z;

// 뺴기
int subtract(int x, int y, int z) => x - y - z;

// 계산
int calculate(int x, int y, int z, Operation operation){
  return operation(x, y, z);
}

```

## 클래스
``` dart
void main() {
  Idol bts = Idol.fromList([
    ['RM', '진', '슈가', '제이홉', '지민', '뷔', '정국'],
    'BTS',
  ]);
  bts.sayHello();

  Idol blackPink = Idol(
    '블랙핑크',
    ['지수', '제니', '리사', '로제'],
  );

  Idol2 blackPink2 = const Idol2(
    '블랙핑크',
    ['지수', '제니', '리사', '로제'],
  );

  print(blackPink == blackPink2); // false

  Idol2 blackPink3 = const Idol2(
    '블랙핑크',
    ['지수', '제니', '리사', '로제'],
  );

  // const를 붙여서 생성한 객체들은 같은 값을 가지고 있으면 같은 인스턴스로 본다.
  print(blackPink2 == blackPink3); // true

  // getter
  print(blackPink.firstMember);

  // setter
  blackPink.firstMember = 'ASAS';
  print(blackPink.firstMember);
}

class Idol {
  String name;
  List<String> members;

  Idol(this.name, this.members);

  Idol.fromList(List values)
      : this.members = values[0],
        this.name = values[1];

  void sayHello() {
    print('${this.name} 입니다. 멤버는 ${this.members}가 있습니다.');
  }

  // getter
  String get firstMember {
    return this.members[0];
  }

  // setter
  set firstMember(String name) {
    this.members[0] = name;
  }
}

class Idol2 {
  final String name;
  final List<String> members;

  const Idol2(this.name, this.members);

  void sayHello() {
    print('${this.name} 입니다. 멤버는 ${this.members}가 있습니다.');
  }
}
```

## 인터페이스
``` dart
// dart는 인터페이스를 생성할 때도 class를 사용한다.
// 하지만 class로만 생성하면 인스턴스화로 생성할 수 있다.
// 인스턴스로 생성 못하게 하려면 abstract키워드를 붙이면 된다.
class IdolInterace{
  String name;
  
  IdolInterace(this.name);
    
  void sayName(){}
}

class BoyGroup implements IdolInterace{
  String name;
  
  BoyGroup(this.name);
  
  void sayName(){}
}
```
