# 김성엽 Project Portfolio

Unity와 C#을 중심으로 산업용 UI, 데이터 관리 애플리케이션과 ROS2 연계 로봇 관제 시스템을 구현한 교육 과정 및 개인 프로젝트 포트폴리오입니다.

## 주요 기술 분야

- Unity 기반 산업용·관제 UI 설계
- C# 데이터 처리와 런타임 상태 관리
- REST API·WebSocket 기반 시스템 연동
- TXT·JSON·CSV·PNG 기반 데이터 저장과 출력
- 로봇 상태·경로·영상·이벤트 시각화

## 프로젝트 목록

| 프로젝트 | 유형 | 핵심 기술 | 상태 |
|---|---|---|---|
| Industrial Kiosk System | 확인 필요 | Unity, C#, TXT, JSON, CSV, PNG | 구현·문서·Windows 빌드 완료 |
| TB3 Smart Factory Control Tower | 5인 팀 프로젝트 | Unity, C#, REST API, WebSocket, ROS2 연계 | 포트폴리오 문서화 완료, 일부 공개 검증 자료 보완 필요 |
| Quik Delivery | 개인 프로젝트 | Unity, C#, JSON, Android | 구현·문서·Android 빌드·GitHub 정리 완료 |

## 프로젝트별 대표 카드

### Industrial Kiosk System

- **한 줄 설명**: 주문·상태·알람·로그와 파일 저장을 하나의 화면에 통합한 Unity 산업용 키오스크입니다.
- **개발 목적**: 산업 현장에서 사용할 수 있는 통합 UI와 로컬 데이터 영속성 흐름을 구현합니다.
- **프로젝트 유형**: 확인 필요
- **담당 역할**: 확인 필요 — 저장소에는 UI 구조, 주문 관리, 저장·로그 및 빌드 구현 범위가 기록되어 있습니다.
- **사용 기술**: Unity, C#, TXT, JSON, CSV, PNG
- **핵심 기능**: 주문 CRUD, 주문번호 생성·검증, 상태·알람 관리, 영수증 PNG, 로그 저장·Export
- **핵심 기술 포인트**: Page Router, `Application.persistentDataPath`, Prefab 기반 반복 Row UI
- **주요 문제와 해결 과정**: 의미 없는 이동·클릭 로그를 제거하고 표시·메모리·저장 로그 수를 제한했습니다.
- **성능 및 안정화**: `TimeDisplay` 1초 갱신, 신규 로그 단건 추가, 영수증 임시 Texture 해제
- **최종 결과**: 데이터 저장·재실행 복원과 Windows Intel 64-bit 빌드를 확인했습니다.
- **대표 이미지**:

<p align="center">
  <img src="assets/projects/industrial-kiosk-system/dashboard.png"
       alt="Industrial Kiosk System Dashboard"
       width="95%">
</p>

- **상세 문서**: [Industrial Kiosk System](docs/projects/industrial-kiosk-system.md)
- **GitHub 저장소**: [kimseongyeop2811-ux/Kiosk](https://github.com/kimseongyeop2811-ux/Kiosk)

### TB3 Smart Factory Control Tower

- **한 줄 설명**: TurtleBot3·ROS2·서버 데이터를 Unity 2D·3D 화면에 연결한 스마트 공장 통합 관제 시스템입니다.
- **개발 목적**: 분산된 로봇 상태, 경로, 영상, 안전 이벤트와 제어 결과를 운영자가 한 화면에서 확인하도록 구성합니다.
- **프로젝트 유형**: 5인 팀 프로젝트
- **담당 역할**: Unity ControlTower UI 설계·구현, REST·WebSocket·Camera Stream 연동, 상태·경로·이벤트·제어 시각화
- **사용 기술**: Unity, C#, REST API, WebSocket, JPEG Camera Stream, ROS2·Nav2 연계
- **핵심 기능**: Dashboard / Factory / Robot / Map / Camera View, Route·Waypoint 추적, 이벤트 Popup, 제어 UI
- **핵심 기술 포인트**: 실제 수신값과 미수신 상태 구분, 로봇별 상태·Route Cache, 좌표 변환
- **주요 문제와 해결 과정**: 화면 재진입 Pose 초기화, 부분 패킷 Route 소실, 영상 연결 상태 오판, Snapshot 덮어쓰기를 캐시와 유효성 관리로 해결했습니다.
- **성능 및 안정화**: 마지막 정상 상태 복원, 실제 JPEG 프레임 기준 상태 판정, 이벤트별 Snapshot Cache 분리
- **최종 결과**: Unity 관제 UI와 팀 서버·ROS2 계층의 데이터 및 명령 흐름을 연동했습니다. 공개 시연 링크와 일부 장비 종단 검증은 보완이 필요합니다.
- **대표 이미지**:

<p align="center">
  <img src="assets/projects/tb3-smart-factory-control-tower/controltower-overview.png"
       alt="TB3 Smart Factory Control Tower"
       width="95%">
</p>

- **상세 문서**: [TB3 Smart Factory Control Tower](docs/projects/tb3-smart-factory-control-tower.md)
- **GitHub 저장소**: [kimseongyeop2811-ux/tb3-smart-factory-control-tower](https://github.com/kimseongyeop2811-ux/tb3-smart-factory-control-tower)

### Quik Delivery

- **한 줄 설명**: 배송 기록, 근무시간, 수익·비용 통계, 달력 조회와 월별 정산·백업을 통합한 Unity 기반 Android 업무 관리 앱입니다.
- **개발 목적**: 실제 배송 업무 데이터를 모바일에서 기록하고 기간별 수익·비용과 정산 결과를 확인할 수 있도록 구성합니다.
- **프로젝트 유형**: 개인 프로젝트
- **담당 역할**: 기획, UI 설계, 데이터 구조, 기능 구현, Android 빌드, GitHub 문서화
- **사용 기술**: Unity, C#, JSON, TextMesh Pro, Android, Native File Picker
- **핵심 기능**: 배송·근무 기록, 수익 계산, 기간별 통계, 부가세 관리, 달력, 월별 정산, 백업·복원
- **핵심 기술 포인트**: UI·Manager·Repository·Service 계층 분리, `Application.persistentDataPath`, 날짜별 데이터 보정
- **주요 문제와 해결 과정**: 배송 0건 날짜에 생성되지 않던 일일 고정비를 기존 기록 변경 없이 누락 날짜에만 추가하고 중복 생성을 방지했습니다.
- **성능 및 안정화**: 전체 데이터 1회 로드·1회 저장, 날짜 `HashSet` 검사, 앱 실행·복귀·자정·백업 복원 진입점 공통화
- **최종 결과**: 기록·통계·달력·정산·백업 기능을 통합하고 Android 실행 및 GitHub 공개 저장소 정리를 완료했습니다.
- **대표 이미지**:

<p align="center">
  <img src="assets/projects/quik-delivery/delivery-input.png"
       alt="Quik Delivery 배송 등록 화면"
       width="55%">
</p>

- **상세 문서**: [Quik Delivery](docs/projects/quik-delivery.md)
- **GitHub 저장소**: [kimseongyeop2811-ux/quik-delivery](https://github.com/kimseongyeop2811-ux/quik-delivery)

## 핵심 역량

- 운영자가 빠르게 판단할 수 있는 산업용·관제 정보 구조 설계
- UI, 데이터, 파일 저장과 통신 책임 분리
- 부분 데이터·미수신·화면 재진입을 고려한 런타임 상태 관리
- 실제 구현, 팀 연동, 검증 보류 범위를 구분하는 문서화
- 기능 구현 이후 저장·복원·빌드와 공개 자료까지 연결하는 마무리

## 기술 스택

| 분류 | 기술 | 적용 프로젝트 |
|---|---|---|
| Engine / UI | Unity, C# | Kiosk, TB3, Quik Delivery |
| Robotics | ROS2, Nav2, TurtleBot3 | TB3 팀 시스템 연계 |
| Programming | C# | Kiosk, TB3, Quik Delivery |
| Data / Communication | TXT, JSON, CSV, PNG | Kiosk |
| Data / Communication | REST API, WebSocket, JPEG Camera Stream | TB3 |
| Data / Storage | JSON, `Application.persistentDataPath` | Quik Delivery |
| Platform | Android | Quik Delivery |
| Collaboration | Git, GitHub | Kiosk, TB3, Quik Delivery |
| Collaboration | Jira, Confluence, Slack | TB3 |

세부 적용 범위와 개인 구현·팀 연동 경계는 [기술 스택 분류](docs/skills.md)에 정리했습니다.

## 문제 해결 중심 개발 방식

1. 화면 증상보다 데이터 소유자와 유효성 조건을 먼저 확인합니다.
2. UI, 저장, 통신 계층의 책임과 실패 지점을 분리합니다.
3. 누락값과 실제 값, 요청 성공과 장치 실행 완료를 구분합니다.
4. 캐시·표시 수·저장 수와 갱신 주기를 조정해 런타임 누적 부담을 줄입니다.
5. 공개 가능한 문서와 이미지로 구현 결과와 검증 한계를 함께 기록합니다.

## 프로젝트 상세 문서 링크

- [Industrial Kiosk System 상세 문서](docs/projects/industrial-kiosk-system.md)
- [TB3 Smart Factory Control Tower 상세 문서](docs/projects/tb3-smart-factory-control-tower.md)
- [Quik Delivery 상세 문서](docs/projects/quik-delivery.md)
- [포트폴리오 문서 안내](docs/README.md)
- [새 프로젝트 작성 템플릿](PROJECT_TEMPLATE.md)

## GitHub 개별 저장소 링크

- [Industrial Kiosk System](https://github.com/kimseongyeop2811-ux/Kiosk)
- [TB3 Smart Factory Control Tower](https://github.com/kimseongyeop2811-ux/tb3-smart-factory-control-tower)
- [TB3 팀 통합 저장소](https://github.com/eduwing-robotics/ros2-ai-amr-repo4)
- [Quik Delivery](https://github.com/kimseongyeop2811-ux/quik-delivery)

## 추후 추가 예정 프로젝트

- PLT Monitor — 로컬 저장소 확인, 다음 카드 작성 대상
- FR5 Digital Twin — 경로·저장소·담당 범위 확인 필요
- LIMO — 경로·저장소·담당 범위 확인 필요

확인되지 않은 기간, 프로젝트 유형, 기여도와 링크는 [추가 확인 항목](docs/open-items.md)에서 관리합니다.
