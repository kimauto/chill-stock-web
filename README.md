# ❄️ Chill Stock - 식자재 전문 3PL 창고 관리 시스템

---


## 🌟 프로젝트 소개
**Chill Stock**은 소상농가와 중·대형 마트를 위한 **콜드체인 기반 마이크로 풀필먼트 WMS**입니다.  
입·출고 요청을 자동 처리하고, 창고·구역 추천·보관 조건 매칭을 통해 **신선도·정확성·편리성·확장성**을 모두 충족합니다.

---

## 👥 팀원

| 이름 (역할)                 | 담당 영역 |
|----------------------------|-----------|
| **김병곤** (devyumi)        | 입고 자동화·실시간 이력·관리자 페이지 |
| 정난희                      | 로그 |
| 정태연                      | 출고 관리 |
| 이정섭                      | 창고/구역 관리, 인프라 연동 |

---

## 💻 화면 구성

### 🔄 동시성 시연 & 입출고 이력 조회

| 동시성 시연 | 입출고 이력 조회 |
|:--:|:--:|
| <img src="https://github.com/user-attachments/assets/9989d3df-9647-47dd-be79-7f8f0c52bab4" width="400"/> | <img src="https://github.com/user-attachments/assets/8dda1d97-5658-4bf7-a28c-fac8d6e4bd37" width="400"/> |

---




## 🧩 주요 기능

| 구분 | 기능 설명 |
|------|-----------|
| **입고 자동화** | Kakao API를 활용해 **거리 + 공간 + 온도 조건**을 만족하는 구역을 추천 → 자동 승인/반려 |
| **반려 사유 처리** | 시스템·관리자 화면에는 **코드(`REJ01`, `REJ02`…)** 저장, 사용자 화면에는 **한글 메시지**로 변환하여 표시 |
| **재고 통합 관리** | 승인 시 재고 테이블 `insert`/`update`, 0개 재고 자동 삭제 |
| **실시간 이력 조회** | `/admin/inventory` 전체 페이지 & `/fragment` AJAX 부분 렌더링 |
| **창고·구역 관리** | 남은 공간 초과 등록 방지, 보관 온도-별 Storage 매칭, 구역 자동 코드 생성 |
| **출고 승인** | 재고-보다 많은 출고량 차단 → 승인 시 재고 차감 & 0개 시 삭제 |
| **보안** | Spring Security 세션(다중 서버 → Redis Session) 기반 인증 |

---

## ⚙️ 개발 환경

| 항목 | 기술 |
|------|------|
| **Backend** | Spring MVC · MyBatis · Spring Security |
| **Frontend** | Thymeleaf · Bootstrap · jQuery(AJAX) |
| **Database** | MySQL · Redis(세션·캐시) |
| **API** | Kakao Map REST API |
| **버전관리 & CI/CD** | GitHub · GitHub Actions(배포 자동화) · Nginx |
| **IDE** | IntelliJ IDEA |

---

## ✨ 김병곤(본인)이 구현한 핵심 모듈

1. **AdminInboundService**  
   - 추천 구역 탐색 → 재고 반영 → 입고 자동 승인 · 반려  
   - 비관적 잠금(`FOR UPDATE`) + `@Transactional`로 동시 승인 충돌 방지

2. **InventoryController**  
   - 전체 페이지 & Fragment 분리 → AJAX 실시간 테이블 렌더링  
   - 페이지네이션 · 총 건수 계산 로직 포함

---

## 📌 향후 개선 로드맵
- WebSocket 기반 이력 push 알림
- 관리자 대시보드 시각화(차트·필터)
- 창고 좌표·거리정보 Redis GEO로 캐싱
- 반려 사유·보관 조건 **enum** 리팩터링
