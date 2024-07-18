# Git Flow

> Git flow는 git에서 branch를 나누는 방법 중 하나이다.

---

## branch 분할

git flow는 branch를 다음 다섯 종류로 나눈다. 이때 master와 develop branch는 필수적으로 필요한 branch이고 나머지는 선택적으로 사용하는 branch이다.

1. master(main)

   제품으로 배포할 수 있는 완성된 branch이다.

2. develop

   master에서 갈라진 branch로, 코드를 상시적으로 commit하는 branch이다. feature에서 개발된 내용을 가지고 있다.

3. feature

   develop에서 갈라진 branch로, 각 기능별로 개발된 내용을 가지고 있는 branch이다. 이때 branch명을 'feat/<기능 이름>' 으로 설정한다.

4. release

   배포 직전 내용을 QA(품질 검사) 하기 위한 branch이다.

5. hotfix

   master로 배포를 하고 나서 버그가 발생하였을 때 이를 빨리 고치기 위한 branch이다.

---
