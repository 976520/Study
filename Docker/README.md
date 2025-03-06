# Docker

> Docker는 linux container에 여러 기능을 추가하여 application을 container로서 더 쉽게 사용할 수 있게 한 프로젝트이다.

Docker는 Go로 개발되어 오픈소스로 꾸준히 업데이트되고 있다.

---

## 기존 가상화와의 차이

기존의 가상화 기술은 hypervisor를 이용해 여러 개의 guest OS를 가상 머신이라는 단위로 구분하여 하나의 host에서 생성해 사용하는 방식이었다. 각 guest OS는 다른 guest OS와 완전히 독립된 독립된 공간에서 자원을 할당받아 사용한다. 하지만 이 작업을 위해 hypervisor를 반드시 거치기 때문에 일반적인 host에 비해 성능적인 손실이 발생할 수 밖에 없다.

Docker container는 가상화된 공간을 생성하기 위해 linux 기능인 chroot, namespace, cgroup를 사용하여, 성능 손실이 거의 없다는 장점이 있다.

---
