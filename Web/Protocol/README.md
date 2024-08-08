## 프로토콜

1. 정의

   > 통신 프로토콜 또는 통신 규약은 컴퓨터나 원거리 통신 장비 사이에서 메시지를 주고 받는 양식과 규칙의 체계이다.

   이는 원활한 통신을 위한 것이다. 예를 들어 한국어를 쓰는 우리가 영어권 사람과 대화하는 것 보다, 한국어를 쓰는 사람끼리 대화하는 것이 더 편할 것이다. 따라서 컴퓨터도 같은 프로토콜을 사용해야 통신이 가능하며, **현존하는 모든 컴퓨터는 후술할 TCP/IP 프로토콜을 사용**한다.

   이 글의 주제인 HTTP도 이러한 프로토콜의 일종으로써, 통신의 규칙을 정한 것이다.

2. 종류

   프로토콜의 대략적인 종류는 다음과 같다.

   1. [**TCP/IP**](https://github.com/976520/TIL/blob/main/network/TCP%2CIP.md) (Transmission Control Protocol / Internet Protocol)

   2. **UDP** (User Datagram Protocol)

      수신 여부를 확인하여 신뢰성이 높지만 속도가 느린 TCP에 비해 수신 여부를 확인하지 않는 UDP는 신뢰성이 낮지만 속도가 빠르다.

   3. **SMTP** (Simple Mail Transfer Protocol)

      간이 우편 전송 프로토콜이라는 이름에서 알 수 있듯이 이메일 전송에 사용되는 네트워크 프로토콜의 한 종류이다.

   4. **HTTP** (Hyper Text Transfer Protocol)

      인터넷상에서 데이터를 빠르게 교환하기 위한 프로토콜이다.

   5. **HTTPS** (Hyper Text Transfer Protocol Secure)

      HTTP의 보안적 약점을 보완하기 위한 프로토콜이다.

---
