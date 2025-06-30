### 250630
# NIC (Network Interface Card)
### <br/><br/>

## 기본 개념
### 아래 블로그에 잘 정리가 되어 있다.
#### https://alluknow.tistory.com/73
### NIC 란?
#### ![image](https://github.com/user-attachments/assets/aee6f5af-fa83-41f3-be84-e3975ab9fd7d)
### <br/>

### NIC 동작
#### ![image](https://github.com/user-attachments/assets/3327f8bc-4344-4703-b122-3a68c1e7337a)
#### <br/>

#### ![image](https://github.com/user-attachments/assets/cc4ad4db-feae-426c-a87f-a069f3408666)
#### <br/>

### 참고로 최근에는 PCIe (PCI express)로 보드 내에서 통신한다.
| 항목       | 설명                                               |
| -------- | ------------------------------------------------ |
| **PCI**  | 오래된 병렬 인터페이스 표준 (90\~2000년대 초반)                  |
| **PCIe** | 최신 직렬 인터페이스 표준 (2004년 이후)                        |
| **공통점**  | 모두 **컴퓨터 내부에서 장치(NIC 등)를 마더보드에 연결하기 위한 버스(Bus)** |
| **차이점**  | PCI는 느리고 병렬, PCIe는 빠르고 직렬 & 레인 기반                |

### <br/><br/>

## 스마트 NIC
#### ![image](https://github.com/user-attachments/assets/c36f608f-63bc-4f7b-bc48-363e0fbd5082)
### <br/><br/>

## 가상 NIC
### **가상 NIC(Virtual NIC)**는 가상 환경(예: VM, 컨테이너, 브리지, 터널 등)에서 사용되는 소프트웨어 기반 네트워크 인터페이스
### 물리적인 네트워크 카드처럼 동작하지만, 실제 하드웨어는 없다.
| 항목    | 설명                                                                         |
| ----- | -------------------------------------------------------------------------- |
| 이름    | Virtual Network Interface Card (vNIC, 가상 NIC)                              |
| 존재 위치 | **가상 머신, 컨테이너, 가상 브리지 등 내부에 존재**                                           |
| 역할    | 물리 NIC처럼 IP 설정, 트래픽 송수신 가능                                                 |
| 생성 주체 | **하이퍼바이저(KVM, VMware)** 또는 **Linux 네트워크 도구** (e.g., `ip`, `docker`, `cni`) |
### <br/>

### 예시
| 환경              | 가상 NIC 예시 이름             | 설명                              |
| --------------- | ------------------------ | ------------------------------- |
| **VM**          | `ens18`, `eth0`          | 하이퍼바이저가 생성한 가상 인터페이스            |
| **Docker 컨테이너** | `eth0`                   | Docker가 생성한 veth pair의 한쪽       |
| **호스트**         | `vethXXXXX`              | 컨테이너 반대편 veth 인터페이스             |
| **브리지**         | `br0`, `docker0`, `cni0` | 여러 NIC를 묶는 가상 스위치               |
| **VPN**         | `tun0`, `tap0`           | 터널 인터페이스 (OpenVPN, WireGuard 등) |
#### <br/>

### 예를 들어 ip addr로 확인하면 docker 같은 경우 이렇게 생겼다
```
3: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether xx:xx:xx:xx:xx:xx brd ff:ff:ff:ff:ff:ff
    inet xx.xx.xx.xx/16 brd xx.xx.xx.xx scope global docker0
       valid_lft forever preferred_lft forever
    inet6 xxxx::xxxx:xxxx:xxxx:xxxx/64 scope link
       valid_lft forever preferred_lft forever
```
### <br/>

### 장점
- 물리 NIC 없이도 트래픽 라우팅 가능
- 성능 테스트, 네트워크 분리, 보안 환경 구축 등에 매우 유용
- Kubernetes 등 분산 시스템에서 Pod 간 통신 구성 핵심 요소
### <br/>

### 주의할 점
- 가상 NIC도 MAC 주소를 갖기 때문에 중복 주의
- 라우팅 설정이 잘못되면 통신 불가
- 외부와 연결하려면 브리지 or NAT 설정 필요
