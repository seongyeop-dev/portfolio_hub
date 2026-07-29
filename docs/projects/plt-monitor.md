# PLT Monitor

## 프로젝트 개요

PLT Monitor는 Unity 생산 라인에서 16개 오브젝트의 Transform 데이터를 실시간으로 기록하고, Overview·Detail·Focus 그래프로 분석하며 JSON·CSV 파일로 저장하는 독립 모니터링 프로젝트입니다.

- **프로젝트 유형**: 교육 과정 과제 기반 개인 프로젝트
- **플랫폼**: Windows Standalone
- **Unity 버전**: 6000.3.10f1
- **담당 범위**: 시스템 구조, Transform 기록, 그래프 UI, 파일 저장·조회, QA, Windows 빌드, GitHub 문서화
- **GitHub**: https://github.com/kimseongyeop2811-ux/PLT_Monitor

## 개발 목적

생산 라인 오브젝트를 직접 제어하는 시스템이 아니라, 움직임을 관찰·기록·분석하는 모니터링 시스템을 구현했습니다.

다음 흐름을 하나의 Unity 대시보드로 구성했습니다.

- 생산 라인 오브젝트 순환
- Transform 실시간 기록
- 다중 대상 비교
- 축별 상세 분석
- 선택 대상 Live View
- 상태·의미·위험도 해석
- JSON·CSV 저장
- 저장 파일 조회와 파싱 결과 확인

## 핵심 결과

| 항목 | 결과 |
|---|---|
| 추적 대상 | Box 16개 |
| 기록 프레임 | 오브젝트당 최근 600개 |
| 기록값 | Position / Rotation / Scale의 X, Y, Z |
| 그래프 모드 | Overview / Detail / Focus |
| 저장 형식 | JSON / CSV |
| 렌더링 | uGUI 기반 그래프 직접 구성 |
| Windows Build | 완료 |

```text
16 Objects × 600 Frames = 9,600 Frames
9 Transform values per frame
= 86,400 Transform values
```

각 프레임은 `frameIndex`, `timeStamp`와 Position·Rotation·Scale의 XYZ 값을 보관합니다.

## 시스템 구조

```text
Transform Recorder
→ Recorder Manager
→ Graph Data Provider
→ UI Controller / Meaning Analyzer
→ Overview / Detail / Focus

Recorder Manager
→ SaveLoad Manager
→ JSON / CSV
→ File Browser
```

- **Recorder**: 대상별 Transform 프레임 수집
- **Recorder Manager**: 16개 대상 기록 통합 관리
- **Graph Data Provider**: 그래프 표시용 데이터 제공
- **Graph Renderer**: 단일·다중 시리즈 선 그래프 렌더링
- **UI Controller**: 대상·Transform 종류·축·분석 모드 전환
- **Meaning Analyzer**: 변화 상태와 위험도를 텍스트로 설명
- **SaveLoad Manager**: JSON·CSV 직렬화 및 파일 저장
- **File Browser**: 저장 파일 목록·선택·파싱 상태 표시

## 주요 기능

### 생산 라인과 기록

- 16개 박스 생산 라인 순환
- Object Pool을 이용한 박스 재사용
- 대상별 Transform Recorder
- 최근 600프레임 롤링 버퍼
- Position·Rotation·Scale의 X·Y·Z 기록

### Overview

16개 박스의 최근 변화를 카드형 미니 그래프로 비교하여 병목, 편차와 정지 여부를 빠르게 탐색합니다.

### Detail

선택한 박스의 X·Y·Z와 All 그래프를 4분면에 표시하여 축별 차이를 비교합니다.

### Focus

선택한 단일 축을 크게 표시하여 변화, 튐, 정지와 노이즈를 자세히 확인합니다.

### Live View

선택된 박스를 카메라가 추적하고 Selected, Metric, Status와 해석 정보를 함께 표시합니다.

### 저장 및 파일 조회

- JSON·CSV Save
- 저장 파일 목록 새로고침
- 파일 선택
- JSON·CSV 파싱 성공 여부 확인
- 상태 메시지 표시

`Load Selected`는 파일 파싱과 성공 여부 확인까지 지원합니다. 로드한 세션을 Recorder에 다시 주입하거나 과거 그래프를 복원하는 기능은 현재 구현 범위에 포함되지 않습니다.

## 주요 문제 해결

### 그래프 갱신 비용 분리

실시간 데이터 수집과 모든 그래프의 매 프레임 재계산을 함께 수행하면 UI 갱신 비용이 커졌습니다.

이를 해결하기 위해 다음 기준을 적용했습니다.

- 데이터 기록과 UI redraw 주기 분리
- Overview·Detail·Focus의 갱신 주기 차등화
- 화면에 필요한 최근 구간만 표시하는 Sliding Window
- 선택 대상과 축이 바뀔 때만 필요한 그래프를 갱신
- Overview에서는 다중 대상 비교, Focus에서는 단일 축 정밀 분석으로 역할 분리

이 구조로 실시간 기록을 유지하면서 화면별 분석 목적과 갱신 비용을 분리했습니다.

### 대규모 Transform 데이터 관리

16개 대상의 전체 기록을 무제한 보관하지 않고 대상별 최근 600프레임을 유지하는 롤링 버퍼 구조를 적용했습니다. 이를 통해 모니터링에 필요한 최근 변화는 유지하면서 메모리 증가를 제한했습니다.

### 저장 순간 성능 저하 문서화

JSON·CSV 저장 시 16 × 600 프레임 집계, 직렬화와 파일 I/O가 메인 스레드에서 함께 수행되어 CPU·GC spike가 발생합니다.

일반 모니터링 구간은 QA 기준을 충족하지만 저장 순간에는 약 40FPS 전후까지 하락한 뒤 회복하는 Known Issue가 있습니다. 문제를 숨기지 않고 원인과 향후 개선 방향을 문서화했습니다.

## 검증 결과

- Unity Console 에러 0개
- 16개 박스 순환과 Recorder 동작 확인
- 일반 실행 60FPS 이상 충족
- 기존 QA 기록상 일반 실행 100FPS 이상
- Overview·Detail·Focus 동작 확인
- 오브젝트·Transform 종류·축 선택 확인
- Live View와 카메라 시점 확인
- JSON·CSV 파일 생성 확인
- 저장 파일 파싱 성공 여부 확인
- Windows Standalone Build 실행 확인

## 대표 화면

<p align="center">
  <img src="../../assets/projects/plt-monitor/overview.png"
       alt="PLT Monitor Overview"
       width="95%">
</p>

## Known Issue와 향후 개선

- JSON·CSV 저장 처리의 비동기화 또는 작업 분할
- 직렬화 전용 데이터 버퍼링
- 로드된 세션의 그래프 재생·비교
- Unity Profiler 원본 캡처 보관
- GitHub Release를 통한 Windows 빌드 제공

## 프로젝트 결과

Transform 데이터 수집, 다중 대상 비교, 축별 상세 분석, 파일 저장과 QA를 하나의 Unity 모니터링 시스템으로 통합했습니다.

이 프로젝트를 통해 실시간 데이터 처리와 UI 갱신 주기의 분리, 롤링 버퍼 기반 데이터 제한, 직접 구현한 그래프 렌더링, 성능 병목의 측정과 Known Issue 문서화 경험을 확보했습니다.
