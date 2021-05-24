AXI(Advanced eXtensible Interface)
====
다중 채널 버스로, 읽기/쓰기에 최적화 되어 있는 버스이다.

 

AXI 버스와 AHB버스의 가장 다른 점은 채널의 도입이다.

- Read Address Channel
- Write Address Channel
- Read Data Channel
- Write Data Channel
- Write Response Channel


 AHB버스의 경우 위의 채널들이 버스로 구성되어 있어 독립적으로 작동할 수 없으나  AXI의 경우에는 채널이 도입되어 독립적으로 작동할 수있다.
 

 AHB버스의 경우 앞의 디바이스가 버스와 데이터 전송을 하고 있는 경우 후속 디바이스가 앞의 데이터 전송이 다 끝날 때 까지 기다려야 했다.
 이는 저속디바이스가 데이터 전송중이라면 고속 디바이스가 데이터 전송을 위해 기다려야 하기 때문에 효율이 떨어졌다.

 하지만 AXI버스의 경우 채널의 도입으로 각자의 채널이 독립적으로 작동 할 수 있어 데이터를 지속적으로 전송할 수 있다.

 

 다음으로는 AXI버스의 데이터 전송방법에 대해 알아보자.

 

*********************************************************************

`valid` : 채널 상에서 유효한 data와 control information 사용 가능 여부

`ready` : 데이터가 수락 가능한지 여부

`last` : transaction에서 마지막 데이터 아이템의 전송을 의미

`BRESP` : transaction이 정상적으로 완료 되었다.

*********************************************************************

초록색은 `master_to_slave` 신호이고파란색 신호는 `slave_to_master` 신호이다.또한 clk는 rising edge에서 활성화 된다.

 

AR은 `Read Address` , 
AW는 `writem Address`. 

R과 W는 DATA에 대한 `R/W`

 

### 1. `master`가 `slave`에 데이터를 전송하는 방법
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F997F93335A0723E508">

1. `master`가 `slave`에게 데이터를 보낼 때 `T2`에서와 같이 address와 control information을 전송한다. 이에 따라 `slave`는 ready신호를 통해 받을 준비가 되었다고 신호를 준다. 이 때 `BREADY` 시그널이 `HIGH`가 된다.
2. ready신호가 `master`에게 전해지게 되면 데이터의 전송이 시작된다
3. `T9`에서 보게 되면 데이터의 전송이 종료 되었으므로 `WLAST`의 값이 전송이 되었다.
4. `WLAST`의 값을 받은 `slave`는 transaction이 완료 되었다는 의미의 `BRESP`신호를 보내게 되고 동시에 `BREADY`의 신호가 `LOW`가 된다.
 
### 2. `slave`가 `master`에게 데이터를 전송하는 방법

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F99B167335A0723E536">
1. `T0`에서 control information(`ARVALID`)의 값이 `HIGH`가 되고 `slave`의 `ARREADY`의 값이 `low`로 바뀌는 순간 address를 전송하고 `ARVALID`의 값은 `low`가 된다.
2. `T3`사이클을 보게 되면 RREADY가 HIGH를 유지하고 있는데 이는 master가 data를 읽을 준비가 되어 있다는 의미이다. `T6`에서 데이터를 전송하자 `RREADY`는 다시 `low`로 떨어진다. 
3. `T7`에서 다시 `RREADY`는 `HIGH`가 되고 앞의 방법과 동일하게 데이터를 읽는다.
4. `T13`에서는 `RLAST`의 값이 `HIGH`가 되어 `slave`의 데이터 전송이 종료 되었음을 알리고 `RREADY`는 `low`가 된다.
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F993BA6335A0723E52C">
위의 그림은 `A`프로세서와 `B`프로세서가 동시에 데이터를 전송하는 모습을 보여준 그래프이다. `A`는 address를 전송해 주지만 data를 모두 전송하지 않은 상태에서 `B`의 address를 전송해 준다. 이 후 `A`의 data가 모두 전송이 된 후 `B`의 데이터가 이어서 전송이 되는 것을 볼 수 있다. 이와 같은 점이 AXI가 채널의 개념을 가짐으로 써 address채널과 data채널이 분리되어 갖는 장점이다.

 

위의 모든 read/write 동작은 모두 `master`에 의해 시작이 된다. 이는 모든 버스의 동작은 항상 `master`에 의해 시작 된다는 것을 알 수 있다.
`master`가 아비터에게서 버스 사용 권한을 획득하여 `valid signal`과 `address signal`을 `slave`에게 보냄으로서 버스의 동작이 실행된다고 볼 수 있다.

 

