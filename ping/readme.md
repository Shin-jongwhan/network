### 250710
## ping은 어떤 도구인가?
### ping은 ICMP (Internet Control Message Protocol) 패킷을 사용해서 네트워크 상의 다른 호스트가 도달 가능한지 확인하는 도구
### layer 3에서 동작하여 TCP / UDP 통신 (layer 4)이 아니기 때문에 포트를 사용하지 않는다.
### 그래서 포트 통신을 확인하려면 layer 4에서 동작하는 도구를 사용해야 한다.
- 기본 목적: 대상이 살아있는지(응답하는지), 지연 시간은 얼마나 되는지 확인
- 기본 동작: ICMP Echo Request → ICMP Echo Reply
### <br/>

### ping은 OSI 모델의 몇 번째 레이어에서 동작할까?
| 특성                | 설명                                       |
| ----------------- | ---------------------------------------- |
| **OSI Layer**     | **Layer 3 (Network Layer)**              |
| **사용 프로토콜**       | ICMP (Internet Control Message Protocol) |
| **IP 기반**         | 맞습니다. IP 주소를 대상으로 동작하며, 포트를 사용하지 않습니다    |
| **TCP/UDP 사용 여부** | ❌ 사용 안 함 (ICMP는 별도의 프로토콜입니다)             |

### <br/>

### Layer 4 (전송 계층)과의 차이점
| 구분    | ping              | TCP/UDP (예: curl, nc, telnet 등)                  |
| ----- | ----------------- | ------------------------------------------------ |
| 레이어   | Layer 3           | Layer 4                                          |
| 프로토콜  | ICMP              | TCP / UDP                                        |
| 포트 사용 | ❌ 사용 안 함          | ✅ 포트 필요                                          |
| 예시    | `ping google.com` | `curl http://google.com:80`, `nc google.com 443` |

### <br/>

## 요약
- `ping`은 **ICMP를 사용하는 Layer 3 네트워크 도구**
- 연결 가능 여부, 패킷 손실, 지연 시간 등을 확인할 수 있음
- **서비스가 죽었는지, 네트워크가 끊겼는지**를 빠르게 파악할 수 있음
- 하지만 웹서버, DB서버 등 **특정 포트의 서비스 확인은 못 함**
### <br/>

### 더 알아보고 싶다면?
- 포트가 열려 있는지 확인: `nc`, `telnet`, `curl`
- DNS 해석만 확인: `nslookup`, `dig`
- traceroute 수준까지 보고 싶다면: `traceroute`, `mtr`
