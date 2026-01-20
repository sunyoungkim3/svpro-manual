# Manual 팝업 화면설계서

**문서 버전**: 1.0  
**작성일**: 2026-01-19  
**목적**: Manual Plate Setting 기능 정의

---

## 1. 개요

### 1.1 화면 목적
SV Pro에서 96-well 또는 384-well Plate를 수동으로 설정하는 팝업입니다. 사용자는 Assay Pack을 선택하고 Consumables를 설정한 후, 필요시 조합검사를 위해 추가 Assay를 선택하여 Plate의 각 Well에 배치할 수 있습니다.

### 1.2 주요 특징
- **자동 Plate 채움**: Base Assay 선택 시 전체 Plate가 자동으로 해당 Assay로 채워짐
- **수동 배치**: 이후 추가 Assay를 선택하여 원하는 Well에 자유롭게 배치 가능
- **Assay Combination**: 최대 3개의 추가 Assay Pack을 Base Assay와 조합 가능
- **드래그 선택**: 마우스 드래그로 여러 Well을 선택하여 Assay 적용
- **Preset 저장**: Admin/Master는 현재 설정을 Preset으로 저장 가능
- **검색 기능**: Assay Pack 검색 지원
- **실시간 시각화**: Plate 설정을 실시간으로 확인 가능

---

## 2. 화면 구조

### 2.1 전체 레이아웃

팝업 크기: 1878px × 900px

**헤더**
- 제목: "Manual"
- 닫기 버튼 [×]

**본문 (2-Column Layout)**

**좌측 섹션**:
1. PCR File Display (읽기 전용)
2. Select Assay Pack (접힌/펼친 상태 지원)
3. Select Consumables (접힌/펼친 상태 지원)
4. Assay Combination (Optional) (접힌/펼친 상태 지원)

**우측 섹션**:
1. Plate Setting (96/384-well)
   - Row labels (96-well: A-H, 384-well: A-P)
   - Column labels (96-well: 1-12, 384-well: 1-24)
   - Plate grid (96 또는 384 wells)
   - Reset 버튼
2. Selected Assay(s) 범례

**푸터**
- Cancel 버튼
- Save as Preset 버튼 (Admin/Master만 표시)
- Start Analysis 버튼

---

## 3. 권한별 기능 제어

### 3.1 권한별 UI 표시

| UI 요소 | User | Admin | Master | 조건 |
|---------|------|-------|--------|------|
| Manual 팝업 진입 | ✓ | ✓ | ✓ | 분석 시작 > Plate Setting: Manual |
| Assay Pack 선택 | ✓ | ✓ | ✓ | 모든 사용자 |
| Consumables 선택 | ✓ | ✓ | ✓ | 모든 사용자 |
| Assay Combination | ✓ | ✓ | ✓ | 모든 사용자 |
| Plate Setting 편집 | ✓ | ✓ | ✓ | 모든 사용자 |
| Reset 버튼 | ✓ | ✓ | ✓ | 모든 사용자 |
| Save as Preset 버튼 | ✗ | ✓ | ✓ | Admin/Master만 |
| Start Analysis 버튼 | ✓ | ✓ | ✓ | 모든 사용자 |

---

## 4. UI 구성요소 상세

### 4.1 PCR File Display

- **타입**: 읽기 전용 정보 표시
- **위치**: 좌측 섹션 최상단
- **구성**:
  - 파일 아이콘
  - "PCR Raw Data:" 레이블
  - 파일명 표시 (예: Sample_PCR_Data_20231226.pcr)

### 4.2 Select Assay Pack

#### Section Header
- **제목**: "Select Assay Pack"
- **기능**: 클릭으로 접기/펼치기
- **요약**: 접힌 상태에서 선택된 Assay 이름 표시

#### Search Box
- **타입**: 텍스트 입력 + 검색 버튼
- **기능**: Assay Pack 이름으로 검색
- **Enter 키**: 검색 실행

#### Assay Pack Table
- **타입**: 테이블
- **컬럼(미정)**: Assay Pack / Category / Compatible / Version / Date
- **선택**: 행 클릭으로 선택
- **선택 표시**: 선택된 행의 모든 셀 배경색 변경
- **데이터**: 각 Assay Pack은 고유 ID와 색상 보유

### 4.3 Select Consumables

#### Section Header
- **제목**: "Select Consumables"
- **표시 조건**: Assay Pack 선택 후 표시
- **초기 상태**: 접힌 상태
- **요약**: 접힌 상태에서 선택된 Consumables 표시

#### Cap/Film Category
- **타입**: 라디오 버튼 그룹
- **옵션**:
  - Standard Cap
  - Optical Film
  - Adhesive Seal
- **기본값**: 첫 번째 옵션 자동 선택, Assay Pack이 선택 된 이력이 있다면 그때 사용했던 옵션으로 자동 선택

#### Plate/Tube Category
- **타입**: 라디오 버튼 그룹
- **옵션**:
  - 8-strip Bio-Rad White Tube
  - Plate Bio Plastics White
  - Plate Bio-Rad White
  - 8-strip Bio Plastics Tube
- **기본값**: 첫 번째 옵션 자동 선택, Assay Pack이 선택 된 이력이 있다면 그때 사용했던 옵션으로 자동 선택

### 4.4 Assay Combination (Optional)

#### Section Header
- **제목**: "Assay Combination (Optional)"
- **표시 조건**: Assay Pack 선택 후 표시
- **초기 상태**: 접힌 상태
- **요약**: 접힌 상태에서 선택된 모든 Assay 이름 표시 (Base + Additional)

#### Description
- "If Assay Combination is required, select additional Assay pack(s) and apply them to wells on the Plate Setting (96/384-well)."

#### Assay List
- **Base Assay 항목**:
  - 고정 표시: "[Assay Name] (Base)"
  - 삭제 버튼 [×] 표시 (클릭 시 모든 설정 초기화)

- **Additional Assay 항목들**:
  - Base Assay를 제외한 모든 Assay Pack 표시
  - Plate에 적용된 Assay는 배경색 변경 및 삭제 버튼 표시
  - 삭제 버튼 클릭 시 해당 Assay가 적용된 Well을 Base Assay로 복원

#### 제약사항
- 최대 3개의 Additional Assay 사용 가능
- Base Assay 포함 총 4개 Assay까지 사용 가능

### 4.5 Plate Setting (96/384-well)

#### Section Header
- **제목**: "Plate Setting"

#### Instruction Text
- **초기 상태**: "Select an assay pack to start"
- **Assay 선택 후**: "Base assay: [Assay Name]. Select an assay to paint on plate."

#### Plate Grid

**96-well Plate:**
- **크기**: 8 rows × 12 columns (96 wells)
- **Row Labels**: A-H (왼쪽)
- **Column Labels**: 1-12 (상단)

**384-well Plate:**
- **크기**: 16 rows × 24 columns (384 wells)
- **Row Labels**: A-P (왼쪽)
- **Column Labels**: 1-24 (상단)

#### 인터랙션
1. **Base Assay 적용**: Assay Pack 선택 시 전체 Well이 자동으로 해당 Assay로 채워짐
2. **Single Click**: 선택된 Assay를 클릭한 Well에 적용
3. **Drag Selection**: 마우스 드래그로 여러 Well 선택하여 Assay 일괄 적용

#### Reset 버튼
- **위치**: Plate Grid 하단 중앙(미정)
- **초기 상태**: 비활성화
- **활성화 조건**: Assay Pack 선택 후
- **기능**: 클릭 시 모든 설정 초기화 (확인 팝업 표시)

#### Selected Assay(s) Legend
- **표시 조건**: Assay Pack 선택 후 표시
- **구성**: 
  - Base Assay 색상 + 이름
  - Additional Assays 색상 + 이름 (Plate에 적용된 것만)

---

## 5. 조건부 표시 규칙

### 5.1 Section 표시 규칙

| Section | 초기 상태 | 표시 조건 |
|---------|----------|----------|
| PCR File Display | 표시 | 항상 표시 |
| Select Assay Pack | 표시 (펼침) | 항상 표시 |
| Select Consumables | 숨김 | Assay Pack 선택 후 표시 (접힌 상태) |
| Assay Combination | 숨김 | Assay Pack 선택 후 표시 (접힌 상태) |
| Plate Setting | 표시 | 항상 표시 |
| Legend | 숨김 | Assay Pack 선택 후 표시 |

### 5.2 버튼 활성화 규칙

| 버튼 | 초기 상태 | 활성화 조건 |
|------|----------|------------|
| Reset | 비활성화 | Assay Pack 선택 후 |
| Save as Preset | 비활성화/숨김 | Assay Pack 선택 후 (Admin/Master만 표시) |
| Start Analysis | 비활성화 | Assay Pack 선택 후 |

### 5.3 Save as Preset 버튼 표시

- **User**: 버튼 자체가 표시되지 않음
- **Admin/Master**: 버튼 표시, Assay Pack 선택 후 활성화

---

## 6. 검증 규칙

### 6.1 Additional Assay 제한

- **조건**: 이미 3개의 Additional Assay가 Plate에 적용됨
- **동작**: 경고 메시지 표시 및 추가 선택 불가

---

## 7. 인터랙션 정의

### 7.1 팝업 열기/닫기

#### 열기
**트리거**:
- 분석 시작하기 > Plate Setting: Manual 선택

**동작**:
1. Manual 팝업 표시
2. PCR 파일 정보 표시
3. Assay Pack 목록 로드
4. 모든 Section 초기 상태로 설정

#### 닫기
**트리거**:
- 닫기 [×] 버튼 클릭
- Cancel 버튼 클릭

**동작**:
1. 확인 팝업 표시
2. 확인 선택 시 팝업 닫기
3. 취소 선택 시 팝업 유지

### 7.2 Assay Pack 선택

**트리거**:
- Assay Pack 테이블에서 행 클릭

**사전 조건**:
- Assay Pack 목록이 로드되어 있어야 함

**동작**:
1. 이전 선택 해제 (테이블에서)
2. 클릭한 행 선택 표시
3. 선택된 Assay를 Base Assay로 저장
4. Consumables Section 표시 및 접힌 상태로 설정
5. Cap/Film, Plate/Tube 기본값 자동 선택 (해당 Assay Pack 선택 이력이 있으면 이전 선택값, 없으면 각각 첫 번째 옵션)
6. Plate 초기화
7. 전체 Plate를 Base Assay 색상으로 채움
8. Assay Combination Section 표시 및 접힌 상태로 설정
9. Combination List에 Base Assay + Additional Assays 표시
10. Reset, Save as Preset, Start Analysis 버튼 활성화
11. Legend 표시
12. Instruction 텍스트 업데이트

**완료 후**:
- Plate 설정을 시작할 수 있는 상태

### 7.3 Consumables 선택

**트리거**:
- Cap/Film 또는 Plate/Tube 라디오 버튼 선택

**동작**:
1. 선택된 옵션 적용
2. Section Summary 업데이트

### 7.4 Additional Assay 선택

**트리거**:
- Assay Combination 목록에서 Assay 항목 클릭

**사전 조건**:
- Base Assay가 선택되어 있어야 함

**동작**:
1. 최대 제한 확인 (Plate에 적용된 Additional Assay가 3개 이상인 경우 경고)
3. 클릭한 항목을 활성 상태로 표시
4. 현재 브러시로 설정
5. Instruction 텍스트 업데이트

**완료 후**:
- Well 클릭 또는 드래그로 선택한 Assay 적용 가능

### 7.5 Plate Well에 Assay 적용

#### Single Click

**트리거**:
- Plate Well 클릭

**사전 조건**:
- 브러시 Assay가 선택되어 있어야 함

**동작**:
1. 브러시 선택 확인 (미선택 시 경고 메시지)
2. 클릭한 Well에 브러시 Assay 색상 적용
3. Plate 데이터 업데이트
5. Legend 업데이트
6. Combination List 항목 상태 업데이트 (삭제 버튼 표시)
7. Summary 업데이트

#### Drag Selection

**트리거**:
- Plate Grid에서 마우스 드래그

**사전 조건**:
- 브러시 Assay가 선택되어 있어야 함

**동작**:
1. 브러시 선택 확인 (미선택 시 경고 메시지)
5. 선택된 모든 Well에 브러시 Assay 색상 적용
6. Plate 데이터 업데이트
8. Legend 업데이트
9. Combination List 항목 상태 업데이트 (삭제 버튼 표시)
10. Summary 업데이트

### 7.6 Additional Assay 삭제

**트리거**:
- Assay Combination 목록의 Assay 항목 삭제 버튼 [×] 클릭

**사전 조건**:
- 해당 Assay가 Plate에 적용되어 있어야 함

**동작**:
1. 확인 팝업 표시
2. 확인 선택 시:
   - Plate에서 해당 Assay가 적용된 모든 Well을 Base Assay로 복원
   - Plate 데이터 업데이트
   - Combination List 항목 상태 업데이트 (삭제 버튼 숨김)
   - 활성 상태 제거
   - Legend 업데이트
   - Summary 업데이트
   - Instruction 텍스트 업데이트

### 7.7 Base Assay 재선택 (다른 Assay Pack 선택)

**트리거**:
- Select Assay Pack 테이블에서 현재 Base Assay와 다른 Assay Pack 선택

**사전 조건**:
- 이미 Base Assay가 선택되어 있는 상태

**동작**:
1. 변경 사항 확인:
   - Consumables 선택이 기본값에서 변경되었는지 확인
   - Additional Assay가 Plate에 적용되었는지 확인
   - 변경 사항이 있는 경우: 확인 팝업 표시
     - 메시지: "Changing the Assay Pack will reset the current configuration. Continue?"
     - 취소 선택 시: 현재 상태 유지, 이전 선택 유지
   - 변경 사항이 없는 경우: 확인 팝업 없이 바로 2번 단계 진행
2. 확인 선택 시 (또는 변경 사항 없는 경우):
   - 모든 선택 상태 초기화
   - 이전 Assay Pack 테이블 선택 해제
   - 새로운 Assay Pack 선택 표시
   - 선택된 Assay를 새로운 Base Assay로 저장
   - Consumables Section은 표시 유지 (접힌 상태)
   - Cap/Film, Plate/Tube 기본값 자동 선택 (새로운 Assay Pack 선택 이력이 있으면 이전 선택값, 없으면 각각 첫 번째 옵션)
   - Assay Combination Section은 표시 유지 (접힌 상태)
   - selectedCombinationAssays 초기화
   - 브러시 해제
   - Plate 초기화
   - 전체 Plate를 새로운 Base Assay 색상으로 채움
   - Legend 업데이트 (새로운 Base Assay만 표시)
   - Combination List에 새로운 Base Assay + Additional Assays 표시
   - Summary 업데이트
   - Instruction 텍스트 업데이트
   - Reset, Save as Preset, Start Analysis 버튼은 활성화 상태 유지

**완료 후**:
- 새로운 Base Assay로 Plate 설정을 시작할 수 있는 상태

### 7.8 Base Assay 삭제 (전체 초기화)

**트리거**:
- Assay Combination 목록의 Base Assay 항목 삭제 버튼 [×] 클릭

**동작**:
1. 변경 사항 확인:
   - Additional Assay가 Plate에 적용되었는지 확인
   - Consumables 선택이 기본값에서 변경되었는지 확인
   - 변경 사항이 있는 경우: 확인 팝업 표시
     - 메시지: "Remove base assay? This will reset everything."
     - 취소 선택 시: 현재 상태 유지
   - 변경 사항이 없는 경우: 확인 팝업 없이 바로 2번 단계 진행
2. 확인 선택 시 (또는 변경 사항 없는 경우):
   - 모든 선택 상태 초기화
   - Assay Pack 테이블 선택 해제
   - Consumables Section 숨김
   - Consumables 선택 해제
   - Assay Combination Section 숨김
   - selectedCombinationAssays 초기화
   - 브러시 해제
   - Plate 초기화
   - Legend 숨김
   - 모든 Section 펼침 상태로 복원
   - Summary 초기화
   - Reset, Save as Preset, Start Analysis 버튼 비활성화
   - Instruction 텍스트 초기화

### 7.9 Reset

**트리거**:
- Reset 버튼 클릭

**사전 조건**:
- Assay Pack이 선택되어 있어야 함 (버튼 활성화 상태)

**동작**:
1. 확인 팝업 표시
2. 확인 선택 시:
   - 모든 선택 상태 초기화
   - Assay Pack 테이블 선택 해제
   - Consumables Section 숨김
   - Consumables 선택 해제
   - Assay Combination Section 숨김
   - selectedCombinationAssays 초기화
   - 브러시 해제
   - Plate 초기화
   - Legend 숨김
   - 모든 Section 펼침 상태로 복원
   - Summary 초기화
   - Reset, Save as Preset, Start Analysis 버튼 비활성화
   - Instruction 텍스트 초기화
   
### 7.10 Save as Preset

**트리거**:
- Save as Preset 버튼 클릭

**사전 조건**:
- Admin 또는 Master 권한
- Assay Pack 선택됨

**동작**:
1. 검증:
   - Assay Pack 선택 확인
2. Preset 이름 입력 다이얼로그 표시
   - 제목: "Save as Preset"
   - 입력 필드: Preset Name (최대 50자)
   - 버튼: Cancel / Confirm
3. Confirm 클릭 시:
   - Preset 이름 입력 확인 (미입력 시 경고)
   - Preset 데이터 구성 및 저장
   - 다이얼로그 닫기
4. Cancel 클릭 시:
   - 다이얼로그 닫기

**Preset 데이터 구성**:
- name: 입력한 Preset 이름
- pcrFile: PCR 파일명
- baseAssay: 선택된 Base Assay
- consumables: Cap/Film, Plate/Tube 선택값
- additionalAssays: Plate에 적용된 Additional Assays
- plateData: well Plate 데이터
**완료 후**:
- Preset 목록 업데이트 (PresetListPopup, Preset Management에 반영)
- 성공 메시지 표시 (선택사항)

### 7.11 Start Analysis

**트리거**:
- Start Analysis 버튼 클릭

**사전 조건**:
- Assay Pack 선택됨

**동작**:
1. 검증:
   - Assay Pack 선택 확인
2. 분석 데이터 구성:
   - pcrFile: PCR 파일명
   - baseAssay: 선택된 Base Assay
   - consumables: Cap/Film, Plate/Tube 선택값
   - additionalAssays: Plate에 적용된 Additional Assays
   - plateData: well Plate 데이터
3. 팝업 닫기

**완료 후**:
- 분석 프로세스 시작

### 7.12 Section 접기/펼치기

**트리거**:
- Section Header 클릭

**동작**:
1. Section의 접힌/펼침 상태 토글
2. 접힌 상태일 때 Summary 표시
3. 펼친 상태일 때 Summary 숨김

---

## 8. 플로우차트

### 8.1 팝업 열기 플로우

```
[Manual 선택]
    ↓
[팝업 열기]
    ↓
[PCR 파일 표시]
    ↓
[Assay Pack 목록 로드]
    ↓
[대기 상태]
```

### 8.2 Plate 설정 플로우

```
[Assay Pack 선택]
    ↓
[Base Assay 설정]
    ↓
[전체 Plate Base Assay로 채움]
    ↓
[Consumables Section 표시]
    ↓
[기본 Consumables 자동 선택]
(이력 있으면 이전 선택값, 없으면 첫 번째 옵션)
    ↓
[Assay Combination Section 표시]
    ↓
    ├→ [Additional Assay 선택 안함] → [Start Analysis]
    │
    └→ [Additional Assay 선택]
        ↓
        [브러시로 설정]
        ↓
        [Plate Well에 적용]
        ↓
        [반복: 다른 Additional Assay 선택 가능]
        ↓
        [Start Analysis]
```

### 8.3 Save as Preset 플로우

```
[Assay Pack 선택됨]
    ↓
[Save as Preset 버튼 활성화]
(미선택 시 버튼 비활성화되어 클릭 불가)
    ↓
[Save as Preset 버튼 클릭]
    ↓
[Preset 이름 입력 다이얼로그]
    ↓
    ├→ [Cancel] → [다이얼로그 닫기]
    └→ [Confirm]
        ↓
        [이름 입력 확인]
        ├→ [미입력] → [경고 메시지]
        └→ [입력됨]
            ↓
            [Preset 데이터 저장]
            ↓
            [Preset 목록 업데이트]
            ↓
            [다이얼로그 닫기]
```

### 8.4 Start Analysis 플로우

```
[Assay Pack 선택됨]
    ↓
[Start Analysis 버튼 활성화]
(미선택 시 버튼 비활성화되어 클릭 불가)
    ↓
[Start Analysis 버튼 클릭]
    ↓
[분석 데이터 구성]
    ↓
[팝업 닫기]
    ↓
[분석 프로세스 시작]
```

### 8.5 Reset/삭제 플로우

```
[Reset 또는 Base Assay 삭제]
    ↓
[확인 팝업]
    ├→ [취소] → [작업 취소]
    └→ [확인]
        ↓
        [모든 상태 초기화]
        ↓
        [Assay Pack 선택 해제]
        ↓
        [Consumables Section 숨김]
        ↓
        [Assay Combination Section 숨김]
        ↓
        [Plate 초기화]
        ↓
        [Legend 숨김]
        ↓
        [버튼 비활성화]
        ↓
        [초기 상태로 복원]
```

---

## 9. 테스트 시나리오

### 9.1 기본 동작 테스트

#### TC-BASIC-001: 팝업 열기 및 초기 상태 확인
**권한**: 모든 사용자
**테스트 단계**:
1. 분석 시작 > Plate Setting: Manual 선택
2. Manual 팝업 표시 확인
3. PCR 파일 정보 표시 확인
4. Assay Pack Section 펼침 상태 확인
5. Consumables Section 숨김 확인
6. Assay Combination Section 숨김 확인
7. Plate Grid 초기화 상태 (빈 상태) 확인
8. Reset 버튼 비활성화 확인
9. Start Analysis 버튼 비활성화 확인
10. Instruction: "Select an assay pack to start" 표시 확인

#### TC-BASIC-002: Assay Pack 선택
**권한**: 모든 사용자
**테스트 단계**:
1. Manual 팝업 열기
2. Assay Pack 테이블에서 첫 번째 Assay 클릭
3. 선택된 행 배경색 변경 확인
4. Consumables Section 표시 및 접힌 상태 확인
5. Cap/Film 기본값 자동 선택 확인 (이력 있으면 이전 선택값, 없으면 첫 번째 옵션)
6. Plate/Tube 기본값 자동 선택 확인 (이력 있으면 이전 선택값, 없으면 첫 번째 옵션)
7. Consumables Summary 표시 확인
8. Assay Combination Section 표시 및 접힌 상태 확인
9. Base Assay 항목 표시 확인
10. Additional Assay 항목들 표시 확인
11. Plate Grid가 Base Assay 색상으로 채워짐 확인
12. Legend 표시 및 Base Assay 정보 확인
13. Reset 버튼 활성화 확인
14. Start Analysis 버튼 활성화 확인
15. Instruction 텍스트 업데이트 확인

#### TC-BASIC-003: Consumables 선택 변경
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨
**테스트 단계**:
1. Consumables Section 펼치기
2. Cap/Film 다른 옵션 선택
3. 선택된 옵션 적용 확인
4. Summary 업데이트 확인
5. Plate/Tube 다른 옵션 선택
6. 선택된 옵션 적용 확인
7. Summary 업데이트 확인

#### TC-BASIC-004: Section 접기/펼치기
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨
**테스트 단계**:
1. Consumables Section Header 클릭
2. Section 펼침 확인
3. Summary 숨김 확인
4. 다시 Header 클릭
5. Section 접힘 확인
6. Summary 표시 확인
7. Assay Combination Section도 동일하게 테스트

#### TC-BASIC-005: 팝업 닫기
**권한**: 모든 사용자
**테스트 단계**:
1. 닫기 [×] 버튼 클릭
2. 확인 팝업 표시 확인
3. 취소 클릭 → 팝업 유지 확인
4. 다시 닫기 버튼 클릭
5. 확인 클릭 → 팝업 닫힘 확인

### 9.2 Assay Combination 테스트

#### TC-COMBINATION-001: Additional Assay 선택 및 적용
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨
**테스트 단계**:
1. Assay Combination Section 펼치기
2. Additional Assay 항목 클릭
3. 항목 활성 상태 표시 확인
4. Instruction 업데이트 확인
5. Plate Well (A1) 클릭
6. Well 색상이 선택한 Assay 색상으로 변경 확인
7. Legend에 Additional Assay 추가 확인
8. Combination List 항목 배경색 변경 및 삭제 버튼 표시 확인
9. Combination Summary 업데이트 확인

#### TC-COMBINATION-002: Drag Selection
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨, Additional Assay 브러시 선택됨
**테스트 단계**:
1. Plate Grid에서 A1부터 A6까지 드래그
2. 드래그 영역 내 모든 Well 색상 변경 확인
3. Legend 업데이트 확인
4. Combination List 항목 상태 업데이트 확인

#### TC-COMBINATION-003: 여러 Additional Assay 적용
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨
**테스트 단계**:
1. 첫 번째 Additional Assay 선택하여 Well A1-A4에 적용
2. Legend에 첫 번째 Assay 추가 확인
3. 두 번째 Additional Assay 선택하여 Well B1-B4에 적용
4. Legend에 두 번째 Assay 추가 확인
5. 세 번째 Additional Assay 선택하여 Well C1-C4에 적용
6. Legend에 세 번째 Assay 추가 확인
7. Plate Grid에 3가지 색상 + Base Assay 색상 표시 확인

#### TC-COMBINATION-004: Additional Assay 최대 제한
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨, 3개의 Additional Assay가 Plate에 적용됨
**테스트 단계**:
1. 네 번째 Additional Assay 선택
2. 경고 메시지 표시 확인

#### TC-COMBINATION-005: Additional Assay 삭제
**권한**: 모든 사용자
**전제조건**: Additional Assay가 Plate에 적용됨
**테스트 단계**:
1. Combination List에서 적용된 Additional Assay의 삭제 버튼 클릭
2. 확인 팝업 표시 확인
3. 취소 클릭 → 작업 취소 확인
4. 다시 삭제 버튼 클릭
5. 확인 클릭
6. 해당 Assay가 적용된 모든 Well이 Base Assay 색상으로 복원 확인
7. Legend에서 해당 Assay 제거 확인
8. Combination List 항목 상태 업데이트 (삭제 버튼 숨김) 확인
9. Summary 업데이트 확인

#### TC-COMBINATION-006: Base Assay 삭제 (전체 초기화)
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨, 일부 Additional Assay 적용됨
**테스트 단계**:
1. Combination List에서 Base Assay의 삭제 버튼 클릭
2. 확인 팝업 표시 확인
3. 확인 클릭
4. Assay Pack 테이블 선택 해제 확인
5. Consumables Section 숨김 확인
6. Assay Combination Section 숨김 확인
7. Plate Grid 초기화 (빈 상태) 확인
8. Legend 숨김 확인
9. 모든 Section 펼침 상태 확인
10. Summary 초기화 확인
11. Reset, Start Analysis 버튼 비활성화 확인
12. Instruction 초기 상태 확인

### 9.3 Reset 테스트

#### TC-RESET-001: Reset 버튼
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨, Plate 일부 수정됨
**테스트 단계**:
1. Reset 버튼 클릭
2. 확인 팝업 표시 확인
3. 취소 클릭 → 작업 취소, 현재 상태 유지 확인
4. 다시 Reset 버튼 클릭
5. 확인 클릭
6. TC-COMBINATION-006의 4-12번 단계와 동일하게 확인

### 9.4 검색 테스트

#### TC-SEARCH-001: Assay Pack 검색
**권한**: 모든 사용자
**테스트 단계**:
1. Search 입력 필드에 "Respiratory" 입력
2. Search 버튼 클릭
3. "Respiratory"가 포함된 Assay만 표시 확인
4. 다른 Assay는 숨김 확인
5. 검색어 지우고 다시 검색
6. 모든 Assay 표시 확인

#### TC-SEARCH-002: Enter 키로 검색
**권한**: 모든 사용자
**테스트 단계**:
1. Search 입력 필드에 "SARS" 입력
2. Enter 키 입력
3. "SARS"가 포함된 Assay만 표시 확인

### 9.5 Save as Preset 테스트

#### TC-PRESET-001: Admin/Master - Save as Preset 버튼 표시
**권한**: Admin 또는 Master
**테스트 단계**:
1. Manual 팝업 열기
2. Save as Preset 버튼 표시 확인
3. 버튼 비활성화 상태 확인
4. Assay Pack 선택
5. 버튼 활성화 확인

#### TC-PRESET-002: User - Save as Preset 버튼 숨김
**권한**: User
**테스트 단계**:
1. Manual 팝업 열기
2. Save as Preset 버튼 숨김 (display: none) 확인
3. Assay Pack 선택 후에도 버튼 표시되지 않음 확인

#### TC-PRESET-003: Preset 저장 - 성공
**권한**: Admin 또는 Master
**전제조건**: Assay Pack 선택됨, Consumables 선택됨, Plate 설정 완료
**테스트 단계**:
1. Save as Preset 버튼 클릭
2. Preset 이름 입력 다이얼로그 표시 확인
3. 제목: "Save as Preset" 확인
4. 입력 필드에 "Test Preset 1" 입력
5. Confirm 버튼 클릭
6. 다이얼로그 닫힘 확인
7. Preset 목록 업데이트 확인 (localStorage 또는 API 확인)

#### TC-PRESET-004: Preset 저장 - 이름 미입력
**권한**: Admin 또는 Master
**전제조건**: Assay Pack 선택됨, Consumables 선택됨
**테스트 단계**:
1. Save as Preset 버튼 클릭
2. Preset 이름 입력 다이얼로그 표시 확인
3. 입력 필드 공백 상태로 Confirm 클릭
4. 경고 메시지 표시 확인
5. 다이얼로그 유지 확인

#### TC-PRESET-005: Preset 저장 - Cancel
**권한**: Admin 또는 Master
**전제조건**: Assay Pack 선택됨, Consumables 선택됨
**테스트 단계**:
1. Save as Preset 버튼 클릭
2. Preset 이름 입력 다이얼로그 표시 확인
3. Cancel 버튼 클릭
4. 다이얼로그 닫힘 확인
5. Preset 저장되지 않음 확인

#### TC-PRESET-006: Preset 저장 - Overlay 클릭
**권한**: Admin 또는 Master
**전제조건**: Assay Pack 선택됨, Consumables 선택됨
**테스트 단계**:
1. Save as Preset 버튼 클릭
2. Preset 이름 입력 다이얼로그 표시 확인
3. Overlay(배경) 클릭
4. 다이얼로그 닫힘 확인

#### TC-PRESET-007: Preset 저장 - Enter 키
**권한**: Admin 또는 Master
**전제조건**: Assay Pack 선택됨, Consumables 선택됨
**테스트 단계**:
1. Save as Preset 버튼 클릭
2. 입력 필드에 "Test Preset 2" 입력
3. Enter 키 입력
4. Preset 저장 확인
5. 다이얼로그 닫힘 확인

### 9.6 Start Analysis 테스트

#### TC-ANALYSIS-001: Start Analysis - 성공
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨, Consumables 선택됨, Plate 설정 완료
**테스트 단계**:
1. Start Analysis 버튼 클릭
2. 분석 데이터 구성 확인
3. 팝업 닫힘 확인

#### TC-ANALYSIS-002: Start Analysis - Assay Pack 미선택
**권한**: 모든 사용자
**테스트 단계**:
1. Manual 팝업 열기 (Assay Pack 선택 안함)
2. Start Analysis 버튼 비활성화 확인
3. (강제로 활성화하여) 버튼 클릭
4. 경고 메시지 표시 확인

#### TC-ANALYSIS-003: Start Analysis - Consumables 미선택
**권한**: 모든 사용자
**전제조건**: Assay Pack 선택됨
**테스트 단계**:
1. Consumables Section에서 모든 라디오 버튼 선택 해제 (강제)
2. Start Analysis 버튼 클릭
3. 경고 메시지 표시 확인

### 9.7 통합 시나리오 테스트

#### TC-INTEGRATION-001: 전체 워크플로우 - Base Assay만
**권한**: 모든 사용자
**테스트 단계**:
1. Manual 팝업 열기
2. Assay Pack 선택
3. Consumables 기본값 확인
4. Start Analysis 클릭
5. 분석 시작 확인

#### TC-INTEGRATION-002: 전체 워크플로우 - Assay Combination
**권한**: 모든 사용자
**테스트 단계**:
1. Manual 팝업 열기
2. Assay Pack 선택
3. Consumables 선택 변경
4. Additional Assay 1 선택하여 Well A1-A6에 적용
5. Additional Assay 2 선택하여 Well B1-B6에 적용
6. Legend 확인 (Base + 2개 Additional)
7. Start Analysis 클릭
8. 분석 시작 확인

#### TC-INTEGRATION-003: 전체 워크플로우 - Save as Preset
**권한**: Admin 또는 Master
**테스트 단계**:
1. Manual 팝업 열기
2. Assay Pack 선택
3. Consumables 선택
4. Additional Assay 적용
5. Save as Preset 클릭
6. Preset 이름 입력
7. Confirm 클릭
8. Preset 저장 확인
9. Start Analysis 클릭
10. 분석 시작 확인

#### TC-INTEGRATION-004: 복잡한 Plate 구성 후 Reset
**권한**: 모든 사용자
**테스트 단계**:
1. Manual 팝업 열기
2. Assay Pack 선택
3. 3개의 Additional Assay를 Plate 여러 위치에 적용
4. Consumables 선택 변경
5. Section 접기/펼치기 여러 번 반복
6. Reset 클릭
7. 확인
8. 모든 상태 초기화 확인

#### TC-INTEGRATION-005: Additional Assay 추가/삭제 반복
**권한**: 모든 사용자
**테스트 단계**:
1. Assay Pack 선택
2. Additional Assay 1 적용
3. Additional Assay 2 적용
4. Additional Assay 1 삭제
5. Legend 및 Plate 업데이트 확인
6. Additional Assay 3 적용
7. Additional Assay 2 삭제
8. Legend 및 Plate 업데이트 확인
9. Start Analysis 성공 확인

---

## 10. 변경 이력

| 버전 | 날짜 | 변경 내용 |
|------|------|----------|
| 1.0 | 2026-01-19 | 초안 작성 |

---

**문서 끝**
