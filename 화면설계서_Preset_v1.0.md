# Preset 팝업 인터랙션 설계서

**문서 버전**: 1.0  
**작성일**: 2026-01-16  
**목적**: Preset 관리 및 선택 기능 정의

---

## 1. 개요

### 1.1 화면 목적
SV Pro 소프트웨어에서 Preset을 조회하고 선택하여 분석을 시작하는 팝업입니다. 사용자는 저장된 Preset 목록을 확인하고, 선택한 Preset의 상세 정보와 Plate 설정을 미리보기할 수 있습니다.

### 1.2 주요 특징
- **Preset 조회**: 저장된 모든 Preset 목록 표시
- **미리보기**: 선택한 Preset의 상세 정보와 well Plate 설정 시각화
- **빠른 분석 시작**: Preset 선택 후 바로 분석 시작 가능
- **실시간 동기화**: Preset Management, Manual 팝업에서 생성/삭제된 Preset 자동 반영

---

## 2. 화면 종류

SV Pro에는 세 가지 Preset 관련 팝업이 있습니다:

### 2.1 Preset 팝업
- **목적**: Preset 선택 및 분석 시작
- **주요 기능**: Preset 목록 조회, 미리보기, 분석 시작

### 2.2 Preset Management 팝업
- **목적**: Preset 관리 (생성/삭제) 및 분석 시작
- **주요 기능**: Preset 목록 조회, Preset 생성/삭제, 미리보기, 분석 시작

### 2.3 Manual 팝업
- **목적**: 수동 Plate 설정 및 분석 시작
- **Preset 관련 기능**: Admin/Master는 Save as Preset 버튼으로 현재 설정을 Preset으로 저장 가능

*참고: Manual 팝업의 전체 화면설계서는 별도 문서로 작성됩니다.*

### 2.4 세 팝업의 차이점

| 구분 | Preset 팝업 | Preset Management 팝업 | Manual 팝업 |
|------|-------------|------------------------|-------------|
| 접근 권한 | 모든 사용자 (User/Admin/Master) | Admin/Master만 | 모든 사용자 |
| 진입 지점 | 분석 시작 > Plate Setting: Preset | 메인 화면 버튼 (Admin/Master만) | 분석 시작 > Plate Setting: Manual |
| Preset 조회 | ✓ | ✓ | ✗ |
| Preset 미리보기 | ✓ | ✓ | ✗ |
| 분석 시작 | ✓ | ✓ | ✓ |
| Preset 생성 | ✗ | ✓ (Admin/Master) | ✓ (Admin/Master) |
| Preset 삭제 | ✗ | ✓ (Admin/Master) | ✗ |
| Add Preset 버튼 | 없음 | Admin/Master 표시 | 없음 |
| Save as Preset 버튼 | 없음 | 없음 | Admin/Master 표시 |
| 삭제 버튼 | 없음 | Admin/Master 표시 | 없음 |
| 주요 목적 | Preset 선택 | Preset 관리 | 수동 Plate 설정 |

---

## 3. 권한별 기능 제어

**중요 사항**:
- **User**: Preset 팝업만 접근 가능. Preset Management 버튼 자체가 표시되지 않아 Preset Management 팝업 내부의 모든 기능을 사용할 수 없습니다.
- **Admin/Master**: 모든 팝업 접근 가능. Preset Management에서 Preset 생성/삭제, Manual에서 Preset 저장 가능.

### 3.1 권한별 UI 표시

| UI 요소 | User | Admin | Master | 조건 |
|---------|------|-------|--------|------|
| Preset 팝업 진입 옵션 | ✓ | ✓ | ✓ | 분석 시작 > Plate Setting |
| Preset Management 진입 버튼 | ✗ (접근 불가) | ✓ | ✓ | 메인 화면 (위치 미정) |
| Manual 팝업 진입 옵션 | ✓ | ✓ | ✓ | 분석 시작 > Plate Setting |
| Add Preset 버튼 | - (팝업 접근 불가) | ✓ | ✓ | Preset Management만 |
| Save as Preset 버튼 | ✗ | ✓ | ✓ | Manual 팝업만 |
| 삭제 [×] 버튼 | - (팝업 접근 불가) | ✓ | ✓ | Preset Management만 |
| Preset 목록 | ✓ (Preset 팝업만) | ✓ | ✓ | Preset / Preset Management |
| Preview 영역 | ✓ (Preset 팝업만) | ✓ | ✓ | Preset / Preset Management |
| Start Analysis 버튼 | ✓ | ✓ | ✓ | 세 팝업 모두 |

---

## 4. 인터랙션 정의

### 4.1 팝업 열기/닫기

#### 열기
- **트리거**:
  1. **분석 시작하기 단계에서 Plate Setting 옵션으로 "Preset" 선택**: Preset 팝업 열기 (모든 사용자)
  2. **분석 시작하기 단계에서 Plate Setting 옵션으로 "Manual" 선택**: Manual 팝업 열기 (모든 사용자)
  3. **메인 화면에서 Preset Management 버튼 클릭**: Preset Management 팝업 열기 (Admin/Master만, 위치 미정)

- **동작**:
  1. 팝업 표시
  2. 저장된 Preset 목록 로드
  3. Preset 목록이 있으면:
     - 첫 번째 Preset 자동 선택
     - Start Analysis 버튼 활성화
  4. Preset 목록이 없으면:
     - "No presets saved yet" 메시지 표시
     - Start Analysis 버튼 비활성화

#### 닫기
- **트리거**: 
  1. 닫기 [×] 버튼 클릭
  2. Cancel 버튼 클릭

- **동작**:
  1. 확인 팝업 표시
  2. 확인 선택 시 팝업 닫기
  3. 취소 선택 시 팝업 유지

### 4.2 Preset 선택

#### 트리거
- Preset 목록에서 Preset 항목 클릭

#### 사전 조건
- Preset 목록이 로드되어 있어야 함

#### 동작
1. 클릭된 Preset 항목에 선택 스타일 적용
2. 이전에 선택된 항목 스타일 제거
3. Preview 영역에 선택된 Preset 정보 표시
4. Start Analysis 버튼 활성화 상태 유지

#### 완료 후
- 선택된 Preset이 변경되고 분석을 시작할 수 있는 상태

### 4.3 Preview 표시

#### Preview 영역 구성

1. **Preset 이름**: 선택된 Preset의 이름 표시
2. **Plate Setting (96-well / 384-well)**: Preset에 저장된 Plate 타입에 따라 표시
   - **96-well**: 8 rows (A-H) × 12 columns
   - **384-well**: 16 rows (A-P) × 24 columns
   - 각 Well은 해당 Assay 색상으로 표시
3. **Selected Assay(s) 범례**: 사용된 Assay 목록과 각각의 색상 표시

### 4.4 Preset 생성

Preset은 두 가지 경로로 생성할 수 있습니다:

#### 방법 1: Preset Management - Add Preset (Admin/Master)

**사전 조건**:
- Preset Management 팝업 접근 가능 (Admin/Master만)
- Add Preset 버튼 표시

**트리거**:
- Preset Management 팝업에서 [+ Add Preset] 버튼 클릭

**동작**:
1. Create Preset 팝업 새 창으로 열기

**Create Preset 완료 후**:
   - Preset 목록 UI 업데이트


#### 방법 2: Manual - Save as Preset (Admin/Master만)

**사전 조건**:
- Manual 팝업 접근 가능 (모든 사용자)
- Save as Preset 버튼 표시 (Admin/Master만, User에게는 숨김)
- Base Assay 선택 완료
- Consumables 선택 완료
- Assay Combination (Optional) 선택 완료
- Plate Setting 선택 완료


**트리거**:
- Manual 팝업에서 [Save as Preset] 버튼 클릭

**동작**:
1. Preset 이름 입력 다이얼로그 표시
   - 다이얼로그 제목: "Save as Preset"
   - 입력 필드: Preset Name (필수)
   - 버튼: Cancel / Save
2. Save 클릭 시:
   - 필수 검증: Preset 이름 입력 여부 확인
   - 이름 미입력 → 경고 메시지: "Please enter a preset name."
   - 이름 입력됨 → Preset 데이터 구성 및 저장
   - 성공 메시지: "Preset saved successfully!"
   - 다이얼로그 닫기
3. Cancel 클릭 시:
   - 다이얼로그 닫기, 작업 취소

**저장 완료 후**:
1. Preset 팝업 및 Preset Management 팝업:
   - Preset 목록 UI 업데이트
2. Manual 팝업:
   - 현재 설정 유지 (초기화하지 않음)
   - Save as Preset 버튼 비활성화 상태

### 4.5 Preset 삭제 (Management - Admin/Master)

#### 사전 조건
- Preset Management 팝업 접근 가능 (Admin/Master만)
- 삭제 버튼 표시

#### 트리거
- Preset 항목 우측 상단의 [×] 버튼 클릭

#### 동작
1. 확인 팝업 표시: "Delete this preset?"
2. 사용자 선택:
   - **취소**: 작업 취소
   - **확인**: 
     1. savedPresets 배열에서 해당 Preset 제거
     2. 데이터 업데이트
     3. 삭제된 Preset이 선택 상태였으면 선택 해제
     4. Preset 목록 UI 업데이트
     5. 남은 Preset 있으면 첫 번째 Preset 자동 선택

#### 완료 후
- Preset 목록이 갱신되고 다른 팝업들도 동기화됨

### 4.6 분석 시작

#### 트리거
- Footer의 [Start Analysis] 버튼 클릭

#### 사전 조건
- Preset이 선택되어 있어야 함 (버튼 활성화 상태)

#### 동작
1. 선택된 Preset 데이터 가져오기
2. 선택된 Preset이 없으면 경고 메시지 표시
3. Assay 목록 구성 (Base Assay + Additional Assays)
4. 백엔드로 분석 데이터 전송
5. 팝업 닫기

#### 완료 후
- 분석 프로세스 시작

---

## 5. 예외 처리 및 에러 메시지

### 5.1 권한 부족

#### Preset Management 접근 시도 (User)
```
진입 지점: 메인 화면에서 Preset Management 버튼이 User에게는 표시되지 않음
결과: 접근 불가 (UI 레벨에서 차단)
```

#### Manual - Save as Preset 시도 (User)
```
진입 가능: Manual 팝업 접근 가능
Save as Preset 버튼: 표시되지 않음
```

### 5.2 데이터 없음

#### Preset 목록 비어있음
```
표시: "No presets saved yet"
위치: Preset 목록 영역 중앙
```

### 5.3 팝업 닫기 확인

#### 닫기 시도 시
```
confirm: "Close the popup?"
- 확인: 팝업 닫기
- 취소: 팝업 유지
```

---

## 6. 테스트 시나리오

### 7.1 기본 동작 테스트

#### 시나리오 1: 팝업 열기 및 닫기
1. 분석 시작하기 > Plate Setting에서 "Preset" 선택 → Preset 팝업 표시 확인
2. [×] 버튼 클릭 → 확인 팝업 표시
3. 확인 클릭 → 팝업 닫기 확인

#### 시나리오 2: Preset 선택 및 미리보기
1. Preset 목록에서 첫 번째 Preset 클릭
2. 선택 스타일 적용 확인
3. Preview 영역에 Preset 정보 표시 확인
4. Plate 그리드 렌더링 확인
5. 범례 표시 확인

#### 시나리오 3: 분석 시작
1. Preset 선택
2. Start Analysis 버튼 활성화 확인
3. Start Analysis 버튼 클릭
4. 팝업 닫힙 확인
5. 분석 프로세스 시작 확인

### 7.2 권한 테스트 (Preset Management)

#### 시나리오 4: Admin/Master 사용자 (Preset Management)
1. Admin 또는 Master 권한일 때
2. 메인 화면에서 Preset Management 버튼 표시 확인
3. Preset Management 접근 가능 확인
4. Add Preset 버튼 표시 확인
5. Preset 항목 삭제 버튼 표시 확인
6. Add Preset 클릭 → Create Preset 창 열림 확인
7. 삭제 버튼 클릭 → 확인 후 Preset 삭제 확인
8. Preset 선택 및 미리보기 정상 동작 확인

#### 시나리오 5: Admin/Master 사용자 (Manual 팝업)
1. Admin 또는 Master 권한일 때
2. Manual 팝업 접근 확인
3. Save as Preset 버튼 표시 확인
4. Base Assay 선택
5. Consumables 선택
6. Plate Setting (96-well) 구성
7. Save as Preset 클릭 → 이름 입력 다이얼로그 표시 확인
8. Preset 이름 입력 후 저장 → 성공 메시지 확인
9. Preset 팝업/Management에서 새로 생성된 Preset 확인

#### 시나리오 6: User 사용자
1. User 권한일 때
2. 분석 시작 > Plate Setting에서 Preset/Manual 옵션 표시 확인
3. 메인 화면에서 Preset Management 버튼 숨김 확인
4. Manual 팝업에서 Save as Preset 버튼 숨김 확인
5. Preset 팝업에서 조회/선택/분석 시작 정상 동작 확인

### 7.3 동기화 테스트

#### 시나리오 7: 창 간 동기화 (Preset 생성)
1. Preset Management 팝업 열기
2. Create Preset 팝업 열기 (새 창)
3. Create Preset에서 Preset 저장
4. Preset Management 목록 자동 갱신 확인
5. 새로 생성된 Preset 표시 확인

#### 시나리오 8: 삭제 동기화
1. 두 개의 Preset Management 창 열기
2. 첫 번째 창에서 Preset 삭제
3. 두 번째 창 목록 자동 갱신 확인
4. 삭제된 Preset 사라짐 확인

### 7.4 예외 상황 테스트

#### 시나리오 9: 데이터 없음
1. Preset 목록이 비어있는 상태에서 팝업 열기
2. "No presets saved yet" 메시지 확인
3. Start Analysis 버튼 비활성화 확인

#### 시나리오 10: 권한 없는 동작 시도 (User)
1. User 권한일 때
2. 분석 시작 > Plate Setting에서 Preset/Manual 옵션 표시 확인 (접근 가능)
3. 메인 화면에서 Preset Management 진입 버튼 숨김 확인
4. Manual 팝업 Save as Preset 버튼 숨김 확인

## 8. 부록

### 8.1 관련 파일

| 파일 | 설명 |
|------|------|
| Preset 팝업 | Preset 선택 및 분석 시작 |
| Preset Management | Preset 관리 (생성/삭제) |
| Create Preset | Preset 생성 팝업 (Management에서 호출) |
| Manual 팝업 | 수동 Plate 설정 및 Preset 저장 (Admin/Master) |

### 8.2 Plate Type 정보

Preset은 생성 시점의 Plate 타입(96-well 또는 384-well) 정보를 포함하며, Preview에서 해당 타입에 맞게 표시됩니다.

| Plate Type | Rows | Columns | Total Wells | Well Size (Preview) |
|-----------|------|---------|-------------|-------------------|
| 96-well | 8 (A-H) | 12 | 96 | 28px × 28px |
| 384-well | 16 (A-P) | 24 | 384 | 14px × 14px |

---

**문서 끝**