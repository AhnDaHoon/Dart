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

  // final은 빌드 타임에 값을 몰라도 된다.
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

## 제너릭
``` dart
void main() {
  Lecture<String, String> lecture1 = Lecture('123', 'asdasd');
  lecture1.printIdType();
  
  Lecture<int, String> lecture2 = Lecture(123, 'asdasd');
  lecture2.printIdType();
}

// generic은 타입을 외부에서 받을때 사용한다.
class Lecture<T, X> {
  final T id;
  final X name;
  
  Lecture(this.id, this.name);
  
  void printIdType(){
    print(id.runtimeType);
  }
}
```

## Iterable타입 형변환
``` dart
void main() {
  List<String> blackPink = ['로제', '지수', '리사', '제니', '제니'];
  print(blackPink.asMap());
  print(blackPink.toSet());
  
  Map blackPinkMap = blackPink.asMap();
  print(blackPinkMap.keys);
  print(blackPinkMap.values);
  
  Set blackPinkSet = Set.from(blackPink);
  print(blackPinkSet.toList());
}
```

## 함수형 프로그래밍
### Collection

#### List
``` dart
void main() {
  List<String> blackPink = ['로제', '지수', '리사', '제니'];
  print(blackPink);
  
  final newBlackPink = blackPink.map((x){
    return '블랙핑크 $x';
  });
  print(newBlackPink);
  
  final newBlackPink2 = blackPink.map((x) =>  '블랙핑크 $x');
  print(newBlackPink2);
  
  print(blackPink == blackPink); // true
  print(blackPink == newBlackPink); // false 
  
  // final 키워드를 붙였고 같은 값이지만 false를 리턴한다.
  // 이유는 map()을 쓰면은 새로운 객체를 생성하기 때문이다.
  print(newBlackPink == newBlackPink2); // false
  
  // [1.jpg, 3.jpg, 5.jpg, 7.jpg, 9.jpg]
  String number = '13579';
  
  final parsed = number.split('').map((x) => '$x.jpg').toList();
  print(parsed);
}
```

#### Map
``` dart
void main() {
  Map<String, String> harryPotter = {
    'Harry Potter': '해리포터',
    'Ron weasley': '론 위즐리',
    'Hermione Granger': '헤르미온느 그레인저'
  };
  print(harryPotter);

  final result = harryPotter.map(
    (key, value) => MapEntry(
        'Harry Potter Character $key',
        '해리포터 캐릭터 $value',
      ),
  );
  print(result);
  
  final keys = harryPotter.keys.map((x) => 'HPC $x').toList();   
  final values = harryPotter.keys.map((x) => '해리포터  $x').toList();
  print(keys);
  print(values);
}
```

#### Set
``` dart
void main() {
  Set blackPinkSet = {
    '로제',
    '지수',
    '제니',
    '리사'
  };
  
  final newSet = blackPinkSet.map((x) => '블랙핑크 $x').toSet();
  print(newSet);
}
```

### reduce
``` dart
void main() {
  List<int> numbers = [1, 3, 4, 7, 9];
  
  // prev 첫번 째 실행인 경우 첫번 쨰 값
  // prev 첫번 째 실행이 아닌 경우 이전에서 리턴한 값
  // next 다음 값
  // reduce는 리턴하는 값이 멤버 변수와 같은 타입이여야 한다.
  final result = numbers.reduce((prev, next){
    print('==========================');
    print('previous: $prev');
    print('next: $next');
    print('total: ${prev + next}');
    
    return prev + next;
  });
  
  print(result);
}
```

### fold
``` dart
void main() {
  List<int> numbers = [1, 3, 4, 7, 9];
  int firstNumber = 0;

  // firstNumber 첫번 째 실행일 떄 넘기는 값
  // prev 첫번 째 실행이 아닌 경우 이전에서 리턴한 값
  // next 다음 값
  final sum = numbers.fold<int>(firstNumber, (prev, next) {
    print('==========================');
    print('previous: $prev');
    print('next: $next');
    print('total: ${prev + next}');

    return prev + next;
  });

  print(sum);
  
  // fold는 reduce와 다르게 리턴값을 멤버변수와 다르게 리턴할 수 있다.
  List<String> words = [
    'a',
    'b',
    'cc',
  ];
  
  final sentence = words.fold<String>('', (prev, next) => prev + next);
  print(sentence);
  
  final count = words.fold<int>(0, (prev, next) => prev + next.length);
  print(count);
}
```

### cascading operator
``` dart
void main() {
  List<int> even = [2, 4, 6, 8];
  List<int> odd = [1, 3, 5, 7];
  
  // cascading operator
  print([...even, ...odd]); // [2, 4, 6, 8, 1, 3, 5, 7]
  print(even == [...even]); // false (cascading operator를 사용하면 새로운 객체를 생성하기 때문에 다른 객체로 나온다.)
}

```

## Async Programming 비동기 프로그래밍

### Future, Future.delayed
``` dart
void main() {
  // Future
  // 미래에 받아올 값
  Future<String> name = Future.value('코드');
  
  addNumbers(1, 1);
  addNumbers(2, 2);
  // 위에 두개 함수 실행 시
  // 계산 시작 : 1 + 1
  // 함수 완료
  // 계산 시작 : 2 + 2
  // 함수 완료
  // 계산 완료: 1 + 1 = 2
  // 계산 완료: 2 + 2 = 4
}

void addNumbers(int n1, int n2){
  print('계산 시작 : $n1 + $n2'); // 첫번째 실행
  
  // delayed
  // 1번 파라미터: 지연할 기간 (얼마나 지연할건지) Duration
  // 2번 파라미터: 지연 시간이 지난 후 실행할 함수 
  Future.delayed(Duration(seconds: 2), (){
    print('계산 완료: $n1 + $n2 = ${n1 + n2}'); // 세번째 실행
  });
  
  print('함수 완료'); // 두번째 실행
}

```

### async, await
``` dart
void main() async {
  await addNumbers2(1, 1);
  await addNumbers2(2, 2);
  // 위에 두개 함수 실행 시
  // 계산 시작 : 1 + 1
  // 계산 완료: 1 + 1 = 2
  // 함수 완료
  // 계산 시작 : 2 + 2
  // 계산 완료: 2 + 2 = 4
  // 함수 완료
}

// await
Future<void> addNumbers2(int n1, int n2) async {
  print('계산 시작 : $n1 + $n2'); // 첫번째 실행
  
  await Future.delayed(Duration(seconds: 2), (){
    print('계산 완료: $n1 + $n2 = ${n1 + n2}'); // 두번째 실행
  });
  
  print('함수 완료'); // 세번째 실행 
}
```

### Future로 리턴값 받기
``` dart
void main() async {  
  final result1 = await addNumbers(1, 1);
  final result2 = await addNumbers(2, 2);
  
  print('result1: $result1');
  print('result2: $result2');
  print('result1 + result2: ${result1 + result2}');
}

// 값을 리턴 하려면 async키워드가 들어가 있어야 한다.
Future<int> addNumbers(int n1, int n2) async {
  print('계산 시작 : $n1 + $n2'); // 첫번째 실행

  await Future.delayed(Duration(seconds: 2), (){
    print('계산 완료: $n1 + $n2 = ${n1 + n2}'); // 세번째 실행
  });
  
  print('함수 완료'); // 두번째 실행
  
  return n1 + n2;
}
```

## Stream
``` dart
import 'dart:async';

void main() {  

  final controller = StreamController();
  final stream = controller.stream.asBroadcastStream();
  
  final streamListener1 = stream.where((val) => val % 2 == 0).listen((val){
    print('streamListener1: $val');
  });
  
  final streamListener2 = stream.where((val) => val % 2 == 1).listen((val){
    print('streamListener2: $val');
  });
  
  controller.sink.add(1);
  controller.sink.add(2);  
  controller.sink.add(3);  
  controller.sink.add(4);  
  controller.sink.add(5);
  
  calculate(2).listen((val){
    print('calculate(2): $val');
  });
  
  calculate(4).listen((val){
    print('calculate(4): $val');
  });

  playAllStream().listen((val){
    print(val);
  });
  
}

Stream<int> calculate(int n) async* {
  for(int i = 0; i < 5; i++){
    yield i * n;
  }
}

Stream<int> playAllStream() async* {
  yield* calculate(1); // yield*을 붙이면 이 함수가 다 끝나고나야 다음 함수가 실행이 된다.(Future의 await와 비슷한 개념)
  yield* calculate(2000);
}
```
