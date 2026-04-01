# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 프로젝트 개요

- **엔진 버전:** Unreal Engine 5.6
- **프로젝트 타입:** Blueprint 전용 (C++ 소스 코드 없음, `Source/` 디렉토리 없음)
- **주요 플러그인:** MetaHuman, MetaHumanCoreTech, MetaHumanCharacter, ModelingToolsEditorMode, EnhancedInput, CommonUI

## 빌드 및 실행

별도의 빌드 스크립트나 Makefile이 없음. 모든 작업은 Unreal Editor를 통해 수행.

- **프로젝트 열기:** `MyProject.uproject`를 더블클릭하거나 Epic Games Launcher에서 열기
- **기본 맵:** `/Game/NaKiUKi/L_Naki`
- **패키징:** Unreal Editor → Platforms → Windows → Package Project

## 코드 아키텍처

### 핵심 게임 구조 (`Content/NaKiUKi/`)

게임의 모든 로직은 이 폴더의 Blueprint에 구현되어 있음.

| Blueprint | 역할 |
|-----------|------|
| `BP_NakiGameMode_C` | 게임 모드 (DefaultGame.ini에 등록됨) |
| `BP_NakiGameInstance_C` | 게임 인스턴스 - 씬 간 데이터 유지 |
| `BP_NakiPlayerController` | 플레이어 컨트롤러 |
| `BP_ClayCharacter` | 조작 가능한 클레이 캐릭터 (물리 애셋, 스켈레탈 메시 포함) |
| `BP_NakiSaveGame` | 세이브/로드 시스템 (`Saved/SaveGames/NakiSlot.sav`) |
| `S_DayRecord` | 일일 기록 데이터 구조체 |

### UI 구조 (CommonUI 프레임워크 사용)

| Widget | 역할 |
|--------|------|
| `WBP_main` | 메인 UI |
| `WBP_Start` | 시작 화면 |
| `WBP_DayRecord` | 일일 기록 UI |
| `WBH_History` | 히스토리 위젯 |

### 입력 시스템

Enhanced Input 사용. `Content/Input/`에 정의됨:
- `IMC_Default` / `IMC_MouseLook` — 입력 매핑 컨텍스트
- `IA_Move`, `IA_Look`, `IA_Jump`, `IA_MouseLook` — 입력 액션
- 터치 입력(`UI_Thumbstick`, `UI_TouchSimple`)도 지원

### 그래픽 설정

DirectX 12, Shader Model 6, 레이 트레이싱 활성화, Virtual Shadow Maps 활성화 (`Config/DefaultEngine.ini`).

## 주의사항

- C++ 파일 수정은 해당 없음 — 모든 로직은 Blueprint로 구현
- 테스트 자동화 인프라 없음 (수동 에디터 테스트)
- `Content/ThirdPerson/`은 UE5 템플릿 기본 콘텐츠 (게임 핵심 로직과 무관)
