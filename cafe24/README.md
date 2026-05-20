# Cafe24 — sidecar 톤 작업 파일

sidecar 메인 사이트(`/index.html`)는 그대로 두고, **shop 페이지만 Cafe24에서 운영**할 때 쓰는 작업 파일 모음.

## 파일

| 파일 | 적용 위치 (Cafe24 스마트디자인) | 설명 |
|---|---|---|
| `shop-list.html` | `/product/list.html` | 상품 목록 페이지 sidecar 톤 |

## 적용 방법

1. Cafe24 관리자 로그인.
2. **디자인 > 디자인 보관함 > 사용 중인 스킨 편집** 진입.
3. 좌측 파일 목록에서 `/product/list.html` 열기.
4. **현재 내용을 다른 곳에 백업** (롤백용).
5. `shop-list.html`의 내용을 **통째로 붙여넣기**.
6. 저장 후 미리보기.

## 적용 후 확인

- 상단/하단(`@layout(/layout/basic/layout.html)`)은 Cafe24 기본 헤더·푸터가 그대로 보임. 다음 단계에서 정리.
- 상품 카드(이미지·이름·가격)는 Cafe24가 자동으로 데이터 채워줌.
- 빈 페이지면 상품을 먼저 1개 이상 등록해야 보임.

## 주의

- `prdList`, `description`, `name`, `price` 같은 클래스명은 Cafe24가 자동 생성하는 마크업.  
  스타일링은 하되 클래스명 자체는 바꾸지 말 것.
- `<!--@layout(...)-->`, `<!--@import(/product/list_product.html)-->`,  
  `<!--@define(cmc_log)-->`는 절대 제거하지 말 것.

## 다음 작업 후보

- `/product/detail.html` — 상품 상세 페이지 sidecar 톤
- `/order/basket.html` — 장바구니
- `/order/orderform.html` — 주문서
- `/layout/basic/layout.html` — 공통 헤더·푸터 sidecar 톤
