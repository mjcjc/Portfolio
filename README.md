# 게임 개발 포트폴리오

C++ 네트워크 서버, 멀티플레이 게임의 서버 콘텐츠, Windows TCP 게임 프로젝트를 정리했습니다.

| 분야 | 프로젝트 | 살펴볼 구현 |
| --- | --- | --- |
| 서버 개발 | [ServerCore](https://github.com/mjcjc/ServerCore) | C++ IOCP 비동기 송수신, 세션과 전송 큐, 서버 역할 분리 |
| 게임 콘텐츠 | [Vida de Granjero](https://github.com/mjcjc/vida_de_granjero) | 농장 게임 서버의 이동 검증, 월드·작물 상태 처리, DB 저장·복원 |
| Windows 프로그래밍 | [2인 멀티플레이 블록 게임](https://github.com/mjcjc/WindowProgrammingTCP) | 2인용 TCP 서버, 보드 상태와 승패 동기화 |

## 서버 개발 · ServerCore

Windows C++와 IOCP를 사용한 멀티 프로세스 채팅 서버입니다. MasterServer는 접속할 서버를 배정하고, GameServer는 세션과 채팅을 처리하며, WorldServer는 채널 간 채팅을 중계합니다.

- **비동기 송수신** — 세션별 수신 버퍼에서 TCP 패킷을 분리하고, 송신 큐에서 부분 송신과 전송 순서를 처리했습니다.
- **전송 큐** — 전송 중인 데이터까지 64KB 한도에 포함하고, 완료 이벤트에서 용량을 반환합니다. 대기 데이터는 다음 전송에 묶어 보냅니다.
- **검증** — SendQueue 테스트 27개 항목을 통과했습니다. 로컬 클라이언트 3개를 사용한 통신 검사에서 송신 100개와 전체 수신 200개를 확인했습니다.

[프로젝트 설명](https://github.com/mjcjc/ServerCore) · [전송 큐 구현](https://github.com/mjcjc/ServerCore/blob/main/TCPServer/SendQueue.cpp) · [테스트 로그](https://github.com/mjcjc/ServerCore/blob/main/docs/evidence/sendqueue-tests.log)

## 게임 콘텐츠 · Vida de Granjero

멀티플레이 농장 게임 졸업작품입니다. 담당 범위는 기존 네트워크 코어 위의 서버 콘텐츠 처리와 클라이언트 연동이었습니다.

- **플레이어 이동** — 서버가 요청 순번과 방향 입력을 검사하고 지형·장애물 조건으로 이동을 검증한 뒤, 처리 결과를 접속 세션에 공유합니다.
- **농장 월드** — 서버에서 월드 오브젝트와 작물 상태를 처리하고 DB 저장·복원을 연동했습니다.

[프로젝트 설명](https://github.com/mjcjc/vida_de_granjero) · [이동 패킷 처리](https://github.com/mjcjc/vida_de_granjero/blob/0f22a28/GameServer/ClientPacketHandler.cpp#L164-L258) · [이동 검증 코드](https://github.com/mjcjc/vida_de_granjero/blob/0f22a28/GameServer/ServerNavigation.cpp)

## Windows 프로그래밍 · 2인 멀티플레이 블록 게임

Windows 환경에서 동작하는 2인용 TCP 게임입니다. 2인용 서버를 설계·구현했고, 두 클라이언트에서 보드 상태와 승패가 다르게 표시되는 문제를 수정했습니다.

[프로젝트 코드](https://github.com/mjcjc/WindowProgrammingTCP)
