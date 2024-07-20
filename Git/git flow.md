# Git Flow

> Git flow는 git에서 branch를 나누는 방법 중 하나이다.

---

## 개념

git flow 전략은 협업 시 소스코드의 관리, 출시를 위한 branch management strategy(브랜치 관리 전략) 의 일종이다.

---

## branch 분할

git flow는 branch를 다음 다섯 종류로 나눈다. 이때 master와 develop branch는 필수적으로 필요한 branch이고 나머지는 선택적으로 사용하는 branch이다.

1. master(main)

   제품으로 배포할 수 있는 완성된 branch이다. 따라서 master에 merge 한다는 것은 서비스의 새로운 버전을 배포한다는 뜻이다.

2. develop

   master에서 갈라진 branch로, 개발자들이 코드를 상시적으로 commit하는 branch이다. feature에서 개발된 내용을 가지고 있다.

3. feature

   develop에서 갈라진 branch로, 각 기능별로 개발된 내용을 가지고 있는 branch이다. 이때 branch명을 'feat/<기능 이름>' 으로 설정한다.
   작업이 완료된 후 develop branch로 merge된다.

4. release

   배포 직전 내용을 QA(품질 검사) 하기 위한 branch이다. 따라서 master branch에 merge한다.

5. hotfix

   master로 배포를 하고 나서 버그가 발생하였을 때 이를 고치기 위한 branch이다. 기본적인 역할은 release branch와 비슷하며, develop에 merge하는 경우도 있지만 이미 배포된 버전에서 발생한 문제를 최대한 빨리 해결해야 하기 때문에 master에 merge하기도 한다.

---
