# sidecar × Cafe24 — 운영 계획

## 최종 결정 (2026-05-20)

지금 sidecar 사이트(youngikyoun.com) 디자인은 **그대로 유지**.
shop 카테고리 클릭 시 → **Cafe24 쇼핑몰로 이동**.
결제·회원·주문관리는 전부 Cafe24가 처리.

## 구조

```
youngikyoun.com  (sidecar — 현재 디자인 그대로)
  ├─ Home / Look / About  (현재 sidecar 그대로)
  └─ Shop 클릭 시
       └→ shop.youngikyoun.com 또는 yge05096.cafe24.com
              (Cafe24 — 상품 분류 페이지로 이동)
```

---

## 다음에 할 일

### 1. sidecar 코드에서 shop 흐름을 외부 링크로 전환

#### 옵션 A — shop 카테고리 자체를 외부 링크로
**파일**: `index.html`
**위치**: 카테고리 버튼 마크업 (`.category--shop`)
**변경 내용**:
- 현재 `<a role="button" tabindex="0" class="category category--shop">`
- 변경 후: `<a href="https://shop.youngikyoun.com/product/list.html?cate_no=33" target="_blank" class="category category--shop">`
- 또는 JS의 `navigateTo('shop')` 분기에서 `window.open(...)`로 빠지게.

**고려할 점**:
- 페이지 전환 overlay 애니매이션 안 보임 (외부 이동이라).
- 새 탭에서 열지(`target="_blank"`), 같은 탭에서 열지 결정.

#### 옵션 B — shop 그리드는 유지, 아이템 클릭 시 외부로
**파일**: `index.html`
**위치**: `openDetail()` 함수 또는 shop-item click 핸들러
**변경 내용**:
- 클릭 시 detail로 가는 대신 `window.open('https://shop.youngikyoun.com/product/detail.html?product_no=10')`로
- 각 sidecar shirt와 Cafe24 product_no 매핑 필요

**고려할 점**:
- sidecar 디자인 더 오래 유지됨
- 매핑 테이블 관리 필요 (sidecar 4개 셔츠 ↔ Cafe24 product_no)

#### 추천
**옵션 A**부터 진행. 단순하고 빠름. 운영 익숙해지면 옵션 B로 진화.

---

### 2. sidecar 코드에서 빼거나 정리할 부분

shop 흐름을 외부에 위임하면 아래는 **사용되지 않음**:
- detail-page 마크업과 관련 JS
- 장바구니 drawer + cart 관련 모든 JS
- checkout 페이지 전체
- 로그인/회원가입 drawer 전부
- order history 등 마이페이지 view들

**처리 방법** 2가지:

**(a) 단순 비활성**: 마크업은 두되 진입 경로만 끊음. 코드 베이스가 무거워지지만 안전.
**(b) 완전 제거**: 코드 베이스 가벼워지고 유지보수 쉬워짐. 단, 한번에 지우지 말고 단계적으로.

추천: **(b) 단계적 제거**. 외부 링크 전환 잘 동작하는 거 확인 후 1주일쯤 두고, 문제 없으면 cart/auth/checkout 관련 코드 일괄 삭제.

---

### 3. Cafe24 쪽 진행 상황

✅ **완료**
- 스킨: 새 루미너스 적용
- 분류: Tops > Shirts (cate_no=33)
- 샘플 상품 등록 + 분류별 진열 → list/detail 페이지에서 정상 표시
- list.html에 sidecar 톤 CSS 입힘 (Cormorant italic, 미니멀)
- detail.html에 sidecar 톤 CSS 입힘
- list.html에서 메인 이동/불필요 요소 제거 CSS 추가

⚠️ **미완 / 알아둘 것**
- 상단 헤더의 “Samplemall” 로고와 카테고리 메뉴(Necklace/Earring 등)는 layout 파일에 있어 list.html CSS만으론 일부만 가려짐
- 상단 띠 배너(쿠폰 안내) 제거 CSS 추가 필요 시 안내함
- main/index.html은 sidecar 톤 미니멀 메인으로 교체했지만, 실제론 사용자가 cafe24 메인을 거의 안 보게 됨
- 한글 라벨(판매가, 배송방법 등) 그대로 — sidecar 톤과 약간 안 어울리지만 한국 운영상 필요

---

### 4. 행정 (실제 판매 시작 전 필수)

⬜ 사업자등록 (홈택스 또는 세무서, 무료)
⬜ 통신판매업 신고 (관할 시·군·구청, 연 4~5만원)
⬜ 구매안전서비스(에스크로) 가입 — Cafe24 통해 PG와 함께 처리
⬜ PG 가맹 신청 — 토스페이먼츠 / 나이스페이 / KG이니시스 등
⬜ 사이트에 사업자 정보 표시 — Cafe24 푸터 영역
⬜ 약관 / 개인정보처리방침 / 환불정책 / 배송정책 페이지 — Cafe24 기본 제공 템플릿 사용

---

### 5. 사용자 경험 (선택, 시간 있을 때)

⬜ shop.youngikyoun.com 서브도메인 연결 (DNS CNAME)
⬜ Cafe24 layout.html의 상단 헤더를 sidecar 톤으로 정리 (로고를 youngik으로, 메뉴 단순화)
⬜ Cafe24 푸터 sidecar 톤 정리
⬜ basket.html (장바구니) sidecar 톤 CSS
⬜ orderform.html (주문서) sidecar 톤 CSS
⬜ 상단 띠 배너(쿠폰) 제거 CSS

---

## 파일 인벤토리

### sidecar (이 프로젝트)
- `index.html` — 메인 sidecar 사이트 (현재 디자인 유지)
- `style.css` — sidecar 스타일
- `cafe24/` — Cafe24 작업 참고용
  - `PLAN.md` — 이 파일
  - `README.md` — Cafe24 작업 안내
  - `shop-list.html` — 초기 list 페이지 작업본 (참고용)

### Cafe24 (admin에서 관리)
- `/main/index.html` — sidecar 톤 미니멀 메인 (youngik + shop 버튼)
- `/product/list.html` — 상품 분류 페이지 (sidecar 톤 적용)
- `/product/detail.html` — 상품 상세 페이지 (sidecar 톤 적용)
- `/layout/basic/layout.html` — 공통 헤더/푸터 (아직 손 안 댐)
- 기타 — 기본 루미너스 그대로

---

## 결제 흐름 요약

```
1. 사용자 → youngikyoun.com (sidecar)
2. 둘러봄 (Home / Look / About / Shop)
3. Shop 클릭 → shop.youngikyoun.com (Cafe24)
4. 상품 선택 → 장바구니 → 결제
5. PG 결제창 → 결제 완료
6. Cafe24 어드민에서 주문 처리 (배송 송장 등록 등)
7. 본인이 택배 발송
```

---

## 핵심 한 줄

> 디자인 자산(sidecar) + 운영 자산(Cafe24)의 분리. 각자 잘하는 일만 함.
