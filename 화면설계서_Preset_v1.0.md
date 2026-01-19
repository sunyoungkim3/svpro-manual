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
- **미리보기**: 선택한 Preset의 상세 정보와 96-well Plate 설정 시각화
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
  3. Preset 목록이 있으면 첫 번째 Preset 자동 선택
  4. Preset 목록이 없으면 "No presets saved yet" 메시지 표시

#### 닫기
- **트리거**: 
  1. 닫기 [×] 버튼 클릭
  2. Cancel 버튼 클릭

- **동작**:
  1. 확인 시 팝업 닫기, 취소 시 팝업 유지

### 4.2 Preset 선택

#### 트리거
- Preset 목록에서 Preset 항목 클릭

#### 동작
1. 클릭된 Preset 항목에 선택 스타일 적용
2. 이전에 선택된 항목 스타일 제거
3. Preview 영역에 선택된 Preset 정보 표시

### 4.3 Preview 표시

#### Preview 영역 구성

1. **Preset 이름**: 선택된 Preset의 이름 표시
2. **Plate Setting (96-well)**: 96-well Plate 그리드 시각화, 각 Well은 해당 Assay 색상으로 표시
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
- Plate Setting (96-well) 선택 완료


**트리거**:
- Manual 팝업에서 [Save as Preset] 버튼 클릭

**동작**:
2. Preset 이름 입력 다이얼로그 표시
   - 다이얼로그 제목: "Save as Preset"
   - 입력 필드: Preset Name (필수)
   - 버튼: Cancel / Save
3. Save 클릭 시:
   - 필수 검증: Preset 이름 입력 여부 확인
   - 이름 미입력 → 경고 메시지: "Please enter a preset name."
   - 이름 입력됨 → Preset 데이터 구성 및 저장
   - 성공 메시지: "Preset saved successfully!"
   - 다이얼로그 닫기
4. Cancel 클릭 시:
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
2. 확인 팝업 표시: "Delete this preset?"
3. 사용자 선택:
   - **취소**: 작업 취소
   - **확인**: 
     5. Preset 목록 UI 업데이트
     6. 남은 Preset 있으면 첫 번째 Preset 자동 선택

### 4.6 분석 시작

#### 트리거
- Footer의 [Start Analysis] 버튼 클릭

#### 사전 조건
- Preset이 선택되어 있어야 함 (버튼 활성화 상태)

#### 동작
1. 선택된 Preset 데이터 가져오기
5. 팝업 닫기

---

## 5. 예외 처리 및 에러 메시지

### 6.1 권한 부족

#### Preset Management 접근 시도 (User)
```
진입 지점: 메인 화면에서 Preset Management 버튼이 User에게는 표시되지 않음
결과: 접근 불가 (UI 레벨에서 차단)
```

#### Manual - Save as Preset 시도 (User)
```
진입 가능: Manual 팝업 접근 가능
Save as Preset 버튼: 표시되지 않음 (display: none 인라인 스타일)
추가 안전장치 (버튼이 보이는 경우): "You don't have permission to save presets."
```

### 5.2 데이터 없음

#### Preset 목록 비어있음
```
표시: "No presets saved yet"
위치: Preset 목록 영역 중앙
```

### 5.3 분석 시작 실패

#### Preset 선택 안 됨
```
alert: "Please select a preset first."
```

#### 선택된 Preset 데이터 없음
```
alert: "Selected preset not found."
```

### 5.4 팝업 닫기 확인

#### 닫기 시도 시
```
confirm: "Close the popup?"
- 확인: 팝업 닫기
- 취소: 팝업 유지
```

---

## 6. 향후 개선 사항

### 6.1 검색 기능
- Preset 목록에서 검색 기능 추가
- 검색 범위: Preset 이름, Assay 이름

### 6.2 정렬 기능
- 생성일 기준 정렬
- 이름 기준 정렬 (A-Z, Z-A)
- 최근 사용 기준 정렬

### 6.3 필터링
- Assay 종류별 필터링
- Consumable 종류별 필터링

### 6.4 편집 기능
- 기존 Preset 편집 (Master만)
- 이름 변경, 설정 수정

### 6.5 복제 기능
- 기존 Preset 복제하여 새 Preset 생성
- 빠른 Preset 생성 지원

### 6.6 즐겨찾기
- 자주 사용하는 Preset 즐겨찾기 표시
- 즐겨찾기 Preset 상단 고정

### 6.7 로딩 인디케이터
- localStorage 로드 시 로딩 표시
- 분석 시작 시 진행 상태 표시

---

## 7. 테스트 시나리오

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
2. Start Analysis 버튼 클릭

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
5. Save as Preset 클릭 → 이름 입력 다이얼로그 표시 확인
6. Preset 이름 입력 후 저장 → 성공 메시지 확인
7. Preset 팝업/Management에서 새로 생성된 Preset 확인

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

---

## 8. 부록

### 8.1 관련 파일

| 파일 | 설명 |
|------|------|
| Preset 팝업 | Preset 선택 및 분석 시작 |
| Preset Management | Preset 관리 (생성/삭제) |
| Create Preset | Preset 생성 팝업 (Management에서 호출) |
| Manual 팝업 | 수동 Plate 설정 및 Preset 저장 (Admin/Master) |

---

**문서 끝**