![Anurag's GitHub stats](https://github-readme-stats.vercel.app/api?username=tjsk002&theme=github_dark&show_icons=true)


# 환경

### 사용스택

TypeScript, ReactJS, Vite, React-router, Axios, React-query, React-Hook-Form, Zod, TailwindCSS

### 실행방법

```bash
pnpm install
```

```bash
pnpm dev
```

# 구현사항

> 구현 기능은 아래 요구 사항을 기반으로 개발해주세요.
> CSS의 경우 필수가 아니며, 기능 중심으로 구현 후 추가적인 사항입니다.

## 유저 게시판 기능 구현

> 리스트 데이터 샘플을 기반으로 CRUD 기능 구현

### [리스트 데이터 샘플]

Mock 데이터는 src/api/mock 폴더의 users-api-data.ts 경로의 usersApiData 사용

```
{
  resultCode: 'A200',
  resultMessage: 'Success',
  resultData: {
    content: [
      {
        username: 'acro1',
        nickName: 'aa',
        gender: 'female',
        isActive: true,
        type: 'back',
        description: 'this is description1',
      },
      ...
    ],
    pageInfo: {
      pageNumber: 1,
      pageSize: 10,
      totalElements: 32,
      totalPages: 4,
    },
  },
}

```

### [리스트 페이지]

1. 초기 페이지 로드 시, mock데이터를 이용해 10개의 게시물을 테이블 형식으로 화면에 표시 (api에서 페이징된 데이터 10개를 받아온다고 가정)
    - isActive의 경우 true이면 ‘활성’, false이면 ‘비활성’으로 표시
    - gender, type의 경우 option label 값으로 표시
2. 페이지네이션 기능 구현
    - 버튼 클릭 시 클릭한 버튼 액티브 기능 구현 (임의 컬러 변경 등)
    - 페이지 변경 시 테이블 데이터 변동은 구현 X, 대신 파라미터로 page 포함해 api 재요청되도록 구현
3. 테이블 상단에 추가 버튼 구현
    - 추가 버튼 클릭 시 신규 데이터 추가페이지로 이동
4. 테이블의 기능 컬럼에 수정, 삭제 버튼 구현
    - 수정 버튼 클릭 시 해당 데이터 수정페이지로 이동
    - 삭제 버튼 클릭 시 해당 데이터 삭제 api 요청
    - 리스트 다시 불러오기

### [생성 페이지]

1. 빈 인풋 표시
2. 저장 클릭 시 생성 api 요청
3. 리스트 페이지로 이동

### [수정 페이지]

1. 해당 데이터의 값을 각 인풋에 표시
2. 저장 클릭 시 수정 api 요청
3. 리스트 페이지로 이동

### [인풋 구성]

> *표시: required <br />
> zod 사용해 유효성 체크 필수 <br />
> 생성, 수정 동일

- *username: text (5~12자리)
- *nickName: text
- gender: radio
    - option label: "Female" | "Male"
    - value: "female" | "male"
- isActive: checkbox
    - value: boolean
- *type: select
    - option label: "Front-end" | "Back-end" | "DBA" | "Infra"
    - value: "front" | "back" | "dba" | "infra"
- description: textarea

### [API 요청]

> 백엔드가 있다고 가정하고 요청까지 구현

데이터는 axios GET 요청 후 반환처리해 사용

- 백엔드 서버 URL: http://acro-test:9000
- 요청 경로
    - GET: /users
    - POST: /users/create
    - PUT: /users/edit
    - DELETE: /users/delete
