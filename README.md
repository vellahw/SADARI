# 독서 모임 기능

Sadari의 독서 모임 기능을 담당해 모임을 만들고, 함께 읽을 사람을 모아 회차별 독서 활동을 이어갈 수 있도록 구현했습니다. 화면 흐름과 서버의 참여·권한 처리를 함께 다룹니다.

## 담당 기능

- 모임 생성, 탐색, 상세 정보 조회와 모임 정보 수정
- 공개·승인제 가입 신청, 초대 및 수락, 모임 탈퇴
- 모임원 관리와 모임장 권한에 따른 관리 기능
- 모임 채팅과 참여자 프로필 이동
- 함께 읽을 도서 투표, 회차별 목표·독서 기록 및 결과 확인
- 가입·초대·승인 과정의 알림과 모임 상태에 따른 사용자 흐름

## 주요 구현

### 정원 초과를 막는 동시성 처리

가입 신청 승인, 바로 가입, 초대 수락이 동시에 들어와도 정원을 넘지 않도록 모임 행을 잠근 뒤 현재 참여 인원과 유효한 초대 예약 인원을 함께 확인합니다. 중복 가입과 모임장 권한도 서버에서 검증합니다.

[독서 모임 동시성 설계](docs/technical-review/reading-club-concurrency.md) · [독서 모임 아키텍처](docs/architecture/reading-club-design.md)

### 모임 중심의 화면 흐름

모임 탐색부터 상세 확인, 가입·초대, 멤버 관리, 채팅, 독서 회차 활동까지 한 모임 안에서 이어지도록 관련 화면과 상호작용을 구현했습니다. 가입 상태와 모임 상태에 따라 사용할 수 있는 기능을 구분합니다.

## 기술

- **Backend:** Java 17, Spring Boot, MyBatis, MySQL
- **Frontend:** React, TypeScript, TanStack Query, Zustand
- **주요 처리:** 트랜잭션, 행 잠금, 권한 검증, 예약 좌석 계산, 알림 연동

## 관련 코드

- 백엔드: `src/main/java/org/our/sadari/readingClub/`
- 프론트엔드 화면: `src/main/frontend/src/pages/ReadingClub/`
- 프론트엔드 기능: `src/main/frontend/src/features/ReadingClub/`
