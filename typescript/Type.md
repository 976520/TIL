# TS의 존재이유

> TypeScript에서는 콜론을 통해 타입을 지정할 수 있다.

---

## 문법

1. 변수

   다음과 같이 변수명의 뒤에 콜론을 붙여 타입을 지정한다.

   ```typescript
   const value: any = "재욱";
   ```

2. 배열

   다음과 같이 배열명의 뒤에 콜론을 붙여 타입을 지정하며, 내부 데이터에 대한 타입을 정의한다.

   ```typescript
   const array: number[] = [11, 22, 33];
   ```

   이를 제네릭 타입을 이용하여 정의하면 다음과 같다.

   ```typescript
   const array: Array<number> = [11, 22, 33];
   ```

   두 방법 사이의 기능적인 차이가 없으므로, 상대적으로 간단한 전자의 방법을 흔히 사용한다.

3. 함수

   콜론을 통해 각각의 매개변수의 타입을 지정할 수 있으며, 소괄호 우측의 콜론을 통해 return값의 타입을 지정할 수 있다. 만약 return값이 없는 함수라면 `void`를 지정한다.

   ```typescript
   function example(param: number): string {
     return `number is ${param}`;
   }
   ```

   각각의 매개 변수에 다른 타입을 지정해도 무관하다. |를 통해 두 타입 중 하나를 선택적으로 받을 수 있으며, 이를 union이라고 한다. 또한 ?:을 통해 인자를 선택적으로 전달할 수 있다.

   ```typescript
   const example = (param1: string | number, param2: string, param3?: boolean): void => {};
   ```

---

## 종류

1. boolean

   true, false 둘 중 하나를 가지게 된다.

   ```typescript
   let isTrue: boolean = false;
   ```

2. number

   숫자라고 해서 C, Java처럼 int, long, float, double 이런거 구별하지 않고, 모든 숫자가 들어갈 수 있다. 이 숫자에는 10진수뿐만 아니라 16진수, 8진수, 2진수 리터럴도 지원한다. 또한 `Infinity`(무한대), `NaN`(Not A Number) 와 같은 요상한 것들도 들어갈 수 있다.

   ```typescript
   let num: number = 0x38a;

   const infinity: number = Infinity;
   const NaN: number = NaN;
   ```

3. string

   ""나 ''으로 감싸진 문자열 뿐만 아니라 ``로 감싸진 ES6 템플릿 문자열도 들어갈 수 있다.

   ```typescript
   let name: string = "재욱";
   let height: string = `${num}cm`;
   ```

4. array

---
