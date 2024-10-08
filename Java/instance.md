# 인스턴스

Instance에 대한 원론적인 설명은 [여기](https://github.com/976520/TIL/blob/main/Java/Object%20Oriented%20Programming/%EA%B0%9C%EB%85%90.md)로 redirect 하겠다.

---

## instance 생성

1. 문법

   `[class명] [변수명] = new [class명]`을 통해 class를 참조하여 새로운 instance를 생성할 수 있다.

2. 사용

   다음과 같이 class로부터 객체를 생성할 수 있다.

   ```java

   public class MakingInstance {
    public static void main(String[] args) {
      Object firstObject = new Object();
      System.out.println("firstObject 변수가 Object 객체를 참조");

      Object secondObject = new Object();
      System.out.println("secondObject 변수가 또 다른 Object 객체를 참조");
    }
   }
   ```

3. instance와 메모리

   위 코드를 실행하면 메모리상에 class 변수와 객체가 생성된다. `Object` class는 하나지만, `new` 키워드를 사용한 만큼 객체가 메모리상에 새로 생성되며, 같은 class를 통해 생성되었지만 각각의 Object 객체는 자신만의 고유 데이터를 가진다. 또한 각 변수가 참조하는 `Object` 객체는 각각 완전히 독립된 서로 다른 객체이다.

---

## instance 멤버

1. 이해

   Instance 멤버란, instance를 생성한 후 사용할 수 있는 field와 method를 뜻하며, 각각 instance field와 instance method 라고 칭한다. 이들은 객체에 소속된 멤버이기 때문에 당연히 객체가 있어야 사용이 가능해진다.

2. `this`

   객체 외부에서 instance 멤버에 접근하기 위해 참조를 이용하는 것과 같이 객체 내부에서는 instance 멤버에 접하기 위해 `this`를 사용한다. `this`는 객체가 자신을 1인칭으로 가리키는 것이다.

3. 사용

   ```java
    class 이주언 {
        int numberOfHairs = 100;

        int 탈모(int numberOfLostHairs) {
            this.numberOfHairs -= numberOfLostHairs;
            return this.numberOfHairs;
        }

        이주언() {
            this.탈모(10);
        }
    }
   ```

   이 코드에서 `numberOfHairs`와 `탈모()`는 각각 instance field와 instance method이다. Class 내부에서 이들을 명확하게 참조하여 사용하기 위해 `this`를 이용한 모습이다.

---
