# Dart

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
