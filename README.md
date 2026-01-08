## GCShop (쇼핑몰) 🛒

Node.js(Express) + MySQL + EJS 기반으로 구현한 쇼핑몰 웹 서비스 **개인 프로젝트**입니다.  
서버에서 화면(EJS)을 렌더링하는 **SSR(Server Side Rendering)** 구조로 개발했으며,  
세션 기반 로그인과 **권한(Guest / Manager)** 에 따른 기능 분리를 구현했습니다.

---

## 📌 Overview

- **Type**: 개인 프로젝트 (대학교 수업 기반 확장)
- **Backend**: Node.js, Express
- **Template Engine**: EJS
- **DB**: MySQL
- **Auth**: express-session + MySQL Session Store
- **Run**: `node main.js` (default: http://localhost:3000)

---

## 🧱 Architecture (SSR + MVC-style)

SSR 환경에서 **역할 분리를 명확히 하기 위해 MVC 스타일로 구조를 설계**했습니다.

- **main.js** : Express 설정 / session 관리 / router mount
- **router/** : 라우팅 (요청 경로 → 컨트롤러 호출)
- **lib/** : 컨트롤러 (비즈니스 로직 + DB Query)
- **views/** : EJS 템플릿 (서버 데이터 기반 화면 렌더링)
- **public/** : 정적 파일 (CSS / Image)

---

## 🗄 Database (MySQL)

**사용 테이블**

- **person** : 회원 (로그인 / 권한 class / grade 포함)
- **product** : 상품
- **cart** : 장바구니
- **purchase** : 구매 내역
- **board, boardtype** : 게시판 / 카테고리
- **code, author, topic, sessions** 등

---

## ✨ Key Features

### 사용자 (Guest)
- 상품 목록 조회 / 검색
- 장바구니 담기 (중복 담기 방지)
- 장바구니 선택 결제 / 선택 삭제
- 구매 내역 조회 / 구매 취소 (cancel flag)

### 관리자 (Manager)
- DB Admin 메뉴 노출
- 상품 관리 (등록 / 수정 / 삭제) 관리자 전용
- person / code / cart / purchase / boardtype 등 관리 화면 접근

---

## 🔐 Authentication & Authorization

- `express-session`을 사용해 로그인 상태를 유지합니다.
- 세션 저장소로 `express-mysql-session`을 사용하여 **세션을 MySQL에 저장**했습니다.
- 사용자 권한(`class`)에 따라 메뉴 및 기능 접근을 분리했습니다.

  - **Guest**: 일반 쇼핑 기능
  - **Manager**: DB Admin (관리 기능)

> 단순 로그인 구현이 아니라, **권한에 따른 UI/기능 분리를 명확히 설계**하는 데 초점을 두었습니다.

---

## 🖼 Screenshots

### Guest View
![Guest](./assets/guest.png)

### Manager (Admin) View
![Manager](./assets/manager.png)

### Database Schema
![DB Schema](./assets/db-schema.png)
