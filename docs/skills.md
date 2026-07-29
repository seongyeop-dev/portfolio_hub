# 기술 스택 분류

기술은 단순 나열하지 않고 실제 프로젝트에서 사용한 목적과 개인 구현·팀 연동 범위를 함께 기록합니다.

## Engine / UI

| 기술 | 적용 프로젝트 | 적용 내용 |
|---|---|---|
| Unity | Kiosk | 산업용 키오스크 화면, Page Router, 반복 Row UI, 영수증 캡처 |
| Unity | TB3 | Dashboard / Factory / Robot / Map / Camera 관제 화면과 2D·3D 시각화 |
| C# | Kiosk | 주문·상태·알람·로그, 파일 저장과 UI Controller |
| C# | TB3 | 관제 UI, 통신 데이터 파싱·캐시·표시와 제어 요청 |

## Robotics

| 기술 | 적용 프로젝트 | 적용 내용 | 범위 |
|---|---|---|---|
| ROS2 | TB3 | 로봇 상태와 명령 계층 연계 | 팀 시스템 연동 |
| Nav2 | TB3 | Route, Waypoint, Goal과 임무 상태 표시 | 팀 시스템 결과 연동 |
| TurtleBot3 | TB3 | 3대 로봇의 상태·위치·영상·제어 UI | 관제 UI 구현 |

ROS2·Nav2 알고리즘과 로봇 하드웨어 자체는 개인 구현 범위로 표시하지 않습니다.

## Programming

| 기술 | 적용 프로젝트 | 적용 내용 |
|---|---|---|
| C# | Kiosk, TB3 | Unity 애플리케이션 로직과 UI 구현 |

현재 1차 카드의 근거만으로 Python을 개인 구현 기술로 표시하지 않습니다.

## Data / Communication

| 기술 | 적용 프로젝트 | 적용 내용 |
|---|---|---|
| TXT | Kiosk | 주문 전체 데이터와 개별 주문서 |
| JSON | Kiosk | 시스템 로그 저장 |
| CSV | Kiosk | 시스템 로그 Export |
| PNG | Kiosk | 영수증 이미지 출력 |
| REST API | TB3 | 초기 조회, 명령 요청, 이벤트 처리 |
| WebSocket | TB3 | 로봇 상태와 이벤트 실시간 수신 |
| JPEG WebSocket | TB3 | Global CCTV와 로봇 카메라 프레임 |

## Modeling

현재 두 프로젝트의 문서만으로 Blender 등 모델링 도구의 직접 사용 범위를 확정할 수 없어 표시를 보류합니다.

## Collaboration

| 기술 | 적용 프로젝트 | 적용 내용 |
|---|---|---|
| Git / GitHub | Kiosk, TB3 | 독립 저장소와 문서·변경 이력 관리 |
| Jira | TB3 | 담당 업무와 진행 상태 관리 |
| Confluence | TB3 | 요구사항·인터페이스·구현 기록 |
| Slack | TB3 | 일정과 인터페이스 조율 |

## 표기 원칙

- `구현`: 직접 작성한 기능과 로직
- `연동`: 다른 파트가 제공한 API·상태·결과를 연결
- `시각화`: 수신 데이터를 UI 또는 2D·3D 공간에 표현
- `확인 필요`: 저장소 문서만으로 직접 사용 여부나 범위를 확정할 수 없음

[문서 안내로 돌아가기](README.md)
## Quik Delivery

- **Engine / UI**: Unity, C#, uGUI, TextMeshPro
- **Data / Storage**: JSON, Application.persistentDataPath
- **Architecture**: UI → Manager → Repository → Service 계층 분리
- **Android**: Native File Picker, 앱 포커스·일시정지·날짜 변경 대응
- **Data Integrity**: HashSet 기반 날짜 중복 방지, 기존 레코드 비변경 누락 보정
- **Validation**: Unity Console, 주요 화면, 월별 정산, 백업 패널 동작 확인
## PLT Monitor

- **Engine / UI**: Unity 6000.3.10f1, C#, uGUI, URP
- **Realtime Data**: 16개 대상 Transform 기록, 대상별 최근 600프레임 롤링 버퍼
- **Visualization**: Overview·Detail·Focus, 다중·단일 시리즈 그래프 직접 렌더링
- **Performance**: 데이터 기록과 UI redraw 주기 분리, Sliding Window, Object Pool
- **Data / Storage**: Newtonsoft.Json, JSON, CSV, File Browser
- **Validation**: Unity Console, 기능 체크리스트, 일반 실행 FPS, Windows Standalone Build

