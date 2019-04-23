# kubernetes

## 용어

**마스터(Master)**
* 클러스터 관리를 담당한다.
* 애플리케이션을 스케줄링하거나, 애플리케이션의 항상성을 유지하거나, 애플리케이션을 스케일링하고, 새로운 변경사항을 순서대로 반영하는 일과 같은 클러스터 내 모든 활동을 조율한다.

**노드(Node)**
* 쿠버네티스 클러스터 내 워커 머신으로써 동작하는 VM 또는 물리적인 컴퓨터다.
* 각 노드는 노드를 관리하고 쿠버네티스 마스터와 통신하는 Kubelet이라는 에이전트를 갖는다.
* 노드는 컨테이너 운영을 담당하는 Docker 또는 rkt와 같은 툴도 갖는다. 운영 트래픽을 처리하는 쿠버네티스 클러스터는 최소 세 대의 노드를 가져야한다.

![Kubernetes cluster](https://user-images.githubusercontent.com/46172074/56556893-259c8e80-65d4-11e9-8787-70af2e574146.PNG)

**디플로이먼트(Deployment)**
* 쿠버네티스가 애플리케이션의 인스턴스를 어떻게 생성하고 업데이트해야 하는지를 지시한다.
* 디플로이먼트가 만들어지면, 쿠버네티스 마스터가 해당 애플리케이션 인스턴스를 클러스터의 개별 노드에 스케줄한다.
* 애플리케이션 인스턴스가 생성되면, 쿠버네티스 디플로이먼트 컨트롤러는 지속적으로 이들 인스턴스를 모니터링한다. 인스턴스를 구동 중인 노드가 다운되거나 삭제되면, 디플로이먼트 컨트롤러가 인스턴스를 클러스터 내부의 다른 노드의 인스턴스로 교체시켜준다.**이렇게 머신의 장애나 정비에 대응할 수 있는 자동 복구(self-healing) 메커니즘을 제공한다.**

![Deployment](https://user-images.githubusercontent.com/46172074/56556913-35b46e00-65d4-11e9-85af-4d4c1afe7d65.PNG)

**파드(Pod)**
* 하나 또는 그 이상의 애플리케이션 컨테이너 (도커 또는 rkt와 같은)들의 그룹을 나타내는 쿠버네티스의 추상적 개념으로 일부는 컨테이너에 대한 자원을 공유한다. 
  * 볼륨과 같은, 공유 스토리지
  * 클러스터 IP 주소와 같은, 네트워킹
  * 컨테이너 이미지 버전 또는 사용할 특정 포트와 같이, 각 컨테이너가 동작하는 방식에 대한 정보
* 파드는 특유한 "로컬호스트" 애플리케이션 모형을 만들어. 상대적으로 밀접하게 결합되어진 상이한 애플리케이션 컨테이너들을 수용할 수 있다.
* 파드는 쿠버네티스 플랫폼 상에서 최소 단위가 된다. 우리가 쿠버네티스에서 배포를 생성할 때, 그 배포는 컨테이너 내부에서 컨테이너와 함께 파드를 생성한다. 각 파드는 스케쥴 되어진 노드에게 묶여지게 된다. 그리고 (재구동 정책에 따라) 소멸되거나 삭제되기 전까지 그 노드에 유지된다. 노드에 실패가 발생할 경우, 클러스터 내에 가용한 다른 노드들을 대상으로 스케쥴되어진다.

![Pod](https://user-images.githubusercontent.com/46172074/56556916-3816c800-65d4-11e9-9b33-d63bdfad0ca9.PNG)

**노드(Node)**
* 파드는 언제나 노드 상에서 동작한다. 노드는 쿠버네티스에서 워커 머신을 말하며 클러스터에 따라 가상 또는 물리 머신일 수 있다. 각 노드는 마스터에 의해 관리된다. 하나의 노드는 여러 개의 파드를 가질 수 있고, 쿠버네티스 마스터는 클러스터 내 노드를 통해서 파드에 대한 스케쥴링을 자동으로 처리한다.
  * Kubelet은, 쿠버네티스 마스터와 노드 간 통신을 책임지는 프로세스이며, 하나의 머신 상에서 동작하는 파드와 컨테이너를 관리한다.
  * (도커, rkt)와 같은 컨테이너 런타임은 레지스트리에서 컨테이너 이미지를 가져와 묶여 있는 것을 풀고 애플리케이션을 동작시키는 책임을 맡는다.

![Node](https://user-images.githubusercontent.com/46172074/56556919-39e08b80-65d4-11e9-8b2c-defdc8d61d08.PNG)

### 관련 용어

**고가용성**
서버와 네트워크, 프로그램 등의 정보 시스템이 상당히 오랜 기간 동안 지속적으로 정상 운영이 가능한 성질을 말한다.

**네트워크 호스트(network host)**
* 컴퓨터 네트워크에 연결된 컴퓨터나 기타 장치이다. 
* 정보 리소스, 서비스, 애플리케이션을 네트워크 상의 사용자나 기타 노드에 제공할 수 있다. 
* 네트워크 주소가 할당된 네트워크 노드이다.
