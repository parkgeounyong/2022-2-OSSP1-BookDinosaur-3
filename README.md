# 2022-02-OSSP1-BookDinosaur-3

=======
> 2022-02 공개SW프로젝트 A+팀
> 
> BookDinosaur 프로젝트
> 
> 기존의 Read Lead 사이트를 보완
>
> https://bookdinosaur.tk/

## Team Member

|학번|이름|역할|
|------|---|---|
|2020112119|강동희|추천시스템알고리즘|
|2019113328|박근용|보안|
|2020110128|박지민|서버,데이터베이스|
|2018112180|정대용|리팩토링,테스팅|

## Tech Stack

<div align=center>
  <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white">
  <img src="https://img.shields.io/badge/css-1572B6?style=for-the-badge&logo=css3&logoColor=white">
  <img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black">
  <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=Node.js&logoColor=white">
  <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=React&logoColor=black">
  <img src="https://img.shields.io/badge/MUI-2196F3?style=for-the-badge&logo=MUI&logoColor=white">
  <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=Express&logoColor=white">
  <br>

  <img src="https://img.shields.io/badge/python-3776AB?style=for-the-badge&logo=python&logoColor=white">
  <img src="https://img.shields.io/badge/scikitlearn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white">
  <img src="https://img.shields.io/badge/MariaDB-003545?style=for-the-badge&logo=MariaDB&logoColor=white">
  <img src="https://img.shields.io/badge/KakaoAPI-FFCD00?style=for-the-badge&logo=Kakao&logoColor=black">
  <img src="https://img.shields.io/badge/docker-2496ED?style=for-the-badge&logo=docker&logoColor=white">
  <img src="https://img.shields.io/badge/nginx-009639?style=for-the-badge&logo=nginx&logoColor=white">
  <img src="https://img.shields.io/badge/oracle cloud-F80000?style=for-the-badge&logo=oracle&logoColor=white">
  <br>

  <img src="https://img.shields.io/badge/Visual Studio Code-007ACC?style=for-the-badge&logo=Visual Studio Code&logoColor=white">
  <img src="https://img.shields.io/badge/git-F05032?style=for-the-badge&logo=git&logoColor=white">
  <img src="https://img.shields.io/badge/github-181717?style=for-the-badge&logo=github&logoColor=white">
</div>

## Environment

### Server

- Node.js 16.14.2
- Express 4.18.1
- MariaDB 8.0.29-0ubuntu0.20.04.3
- Nginx 1.23.1

### Client
- React 17.0.2


## Main Feature

### Recommend System

**1. SVD recommend system**
- 유저-평점 행렬을 SVD 분해하여 특이값을 얻어내고, 이를 바탕으로 예측 평점 계산
- 계산한 예측 평점이 높은 순으로 추천 도서 제공
<img src="https://user-images.githubusercontent.com/83688807/173960562-afb2069b-cc08-458e-85cc-069bad0d8a8a.png"  width="30%" height="30%"/>
<br>

**2. Cosine Similarity recommend system**
- 회원가입 시 유저에게 도서 분류별 관심도 정보 받아 계산
- 방향적인 유사도 정보를 위해 코사인 유사도 활용
- 나와 유사한 집합에서 평점 평균이 높은 순으로 추천 도서 제공
<img src="https://user-images.githubusercontent.com/83688807/173960573-b8d0cefb-c71b-4b0f-817f-8a7f17a1131b.png"  width="30%" height="30%"/>


### Page
**1. Login page**

![Loginpage](https://user-images.githubusercontent.com/83688807/173960048-0095d697-658e-4765-8e64-bbf409d9fe81.PNG)
- 아이디와 비밀번호를 사용하여 로그인
<br>

## Requirements

-   주어진 API에 맞는 DB 서버
-   카카오 API 키, DB 설정값, 세션 secret 정보 관련 환경변수 파일(.env)

### .env 원형

```
PUBLIC_URL=
SESSION_SECRET=
PORT=3000

# DATABASE(MARIADB)
MARIADB_ROOT_PASSWORD=
MARIADB_USER=
MARIADB_PASSWORD=
TZ=Asia/Seoul

DB_PORT=3306
DB_NAME=BOOKWEB
DB_HOST=database

# KAKAO
KAKAO_API_KEY=
```

### DB Schema

```
CREATE DATABASE BOOKWEB;

USE BOOKWEB;

CREATE TABLE BookTB (
    Id INT PRIMARY KEY,
    title VARCHAR(100) NOT NULL,
    information VARCHAR(100) NOT NULL,
    genres VARCHAR(100) NOT NULL
);

CREATE TABLE UserTB (
    userid VARCHAR(25) PRIMARY KEY,
    password VARCHAR(60) NOT NULL,
    nickname VARCHAR(25) NOT NULL,
    age INT NOT NULL,
    sexuality VARCHAR(25) NOT NULL,
    preference VARCHAR(50) NOT NULL
);

CREATE TABLE BookReportTB (
    userid VARCHAR(25) NOT NULL,
    isbn VARCHAR(24) NOT NULL,
    title VARCHAR(100) NOT NULL,
    contents VARCHAR(300) NOT NULL,
    rating VARCHAR(5) NOT NULL,
    date DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,
    views INT NOT NULL DEFAULT 0,
    CONSTRAINT FK_userid
    FOREIGN KEY (userid) REFERENCES UserTB (userid),
    CONSTRAINT FK_isbn
    FOREIGN KEY (isbn) REFERENCES BookTB (isbn)
);

CREATE TABLE RatingTB (
    User_id INT PRIMARY KEY,
    book_id INT NOT NULL,
    Rating INT NOT NULL
);
```
