# CSMA-CD

> CSMA/CD는 Carrier Sense Multiple Access/Collision Detection의 약자로, 통신 방식의 일종이다.

한 마디로 대충 알잘딱 통신하자 이다.

여러 system이 동시에 통신을 하게되면 문제가 발생할 수 있는데, 이 부분을 어떠한 방식으로 처리 하는지에 대한 것이다. 일반적으로 느끼기에 동시에 통신을 해도 충돌은 발생하지 않는데? 라고 생각할 수 있지만, 하나의 [[Ethernet]]([[LAN]]) 회선에서는 우리가 체감할 수 없는 아주 짧은 시간에 데이터 송/수신을 제어 및 처리를 하여 통신을 하게된다.

## Carrier Sense

Ethernet 환경에서 통신하려는 system은 먼저 현재 network에서 다른 장치가 통신 중인지 확인해야 한다. 즉, 네트워크 자원을 사용하고 있는 PC나 서버의 존재 여부를 확인하는 과정이 필요하다.

송신 장치는 케이블을 통해 전달되는 신호를 감지하여 다른 장치의 데이터 전송이 진행 중인지 확인하고, 통신이 이루어지고 있지 않을 때 전송을 시작한다. 이처럼 전송 매체에 신호(carrier)가 존재하는지를 확인하는 과정을 **Carrier Sense**라고 한다.

만약 carrier가 감지되면 보내고자 하는 data가 있어도 일단 대기한다. 그러다가 통신이 없어져서 carrier가 감지되지 않으면 전송을 시작한다.

## Multiple Access

만약 network상에서 두 PC가 carrier가 감지되지 않은 것을 확인하고 곧바로 data를 보낸다면 두 PC가 동시에 data를 보내게 된다. 

Ethernet에서는 이렇개 둘 이상의 system이 동시에 network상에 data를 보내는 경우를 다중 접근, Multile Access라고 한다.

## Collision Detection

이처럼 두 개의 system이 동시에 데이터를 전송하려고 하여 신호가 충돌하는 상황을 **collision**이 발생했다고 한다. 따라서 Ethernet에서는 데이터를 network로 전송한 이후에도 다른 system의 전송과 충돌이 발생하지 않았는지 지속적으로 확인해야 한다. 이러한 과정을 **Collision Detection**이라고 한다.

<img width="1867" height="756" alt="Image" src="https://github.com/user-attachments/assets/9a68f3ad-0f88-4371-bba8-236b0c138818" />

송신 장치는 data를 전송하는 동안에도 전송 매체의 신호를 감시하여 다른 장치의 송신과 collision이 발생하는지 확인한다. 만약 **collision**이 발생하면 충돌 사실을 감지한 후 현재 전송을 중단한다. 이후 각 송신 장치는 매우 짧은 랜덤 시간 동안 대기한 뒤 다시 전송을 시도한다. 이때 각 장치의 대기 시간이 서로 다르므로 동일한 시점에 재전송할 가능성을 줄일 수 있다.

재전송에서도 다시 **collision**이 발생할 수 있으며, 이 경우에는 또다시 일정 시간 대기한 후 전송을 재시도한다. Ethernet은 이러한 과정을 반복하며, 일반적으로 최대 16회(최초 전송 포함)까지 전송을 시도한다. 그 이후에도 전송에 실패하면 해당 전송을 포기하고 오류로 처리한다.