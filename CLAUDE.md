# NocoBase 2.0 Menu, Page, Block 생성 API 가이드

## 시스템 정보
- NocoBase 버전: 2.0.0-alpha.39
- API Base URL: `http://localhost:22001/api/`
- 인증: Bearer Token 필요

## 인증 (251119 업데이트)

현재 사용 가능한 인증 토큰:

```bash
# API Key 정보
API_KEY_NAME=local-jeonghan-251119
API_KEY_VALUE=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4

# API 호출 시 헤더에 추가
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4
```

## 1. 메뉴 관리 API

### 메뉴 생성
```bash
POST /api/uiSchemas
```

메뉴 생성 예시:
```bash
curl -X POST http://localhost:22001/api/uiSchemas \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "void",
    "name": "menu_item_name",
    "title": "메뉴 제목",
    "x-component": "Menu.Item",
    "x-server-hooks": [],
    "properties": {
      "page": {
        "type": "void",
        "x-component": "Page",
        "x-async": true,
        "properties": {}
      }
    }
  }'
```

### 메뉴 조회
```bash
curl -X GET "http://localhost:22001/api/uiSchemas?filter[name]=menu_item_name" \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4"
```

### 메뉴 수정
```bash
curl -X PATCH http://localhost:22001/api/uiSchemas/:id \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4"
```

### 메뉴 삭제
```bash
curl -X DELETE http://localhost:22001/api/uiSchemas/:id \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4"
```

## 2. 페이지 생성 API

### 페이지 스키마 생성
```bash
curl -X POST http://localhost:22001/api/uiSchemas \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "void",
    "name": "page_name",
    "title": "페이지 제목",
    "x-component": "Page",
    "x-app": true,
    "properties": {
      "grid": {
        "type": "void",
        "x-component": "Grid",
        "x-initializer": "page:addBlock",
        "properties": {}
      }
    }
  }'
```

### 페이지 조회
```bash
curl -X GET "http://localhost:22001/api/uiSchemas?filter[x-component]=Page" \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4"
```

## 3. 블록 생성 API

### 테이블 블록 생성
```bash
curl -X POST http://localhost:22001/api/uiSchemas \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "void",
    "x-component": "Grid.Row",
    "properties": {
      "block": {
        "type": "void",
        "x-component": "Grid.Col",
        "properties": {
          "table": {
            "type": "void",
            "x-decorator": "TableBlockProvider",
            "x-component": "CardItem",
            "x-decorator-props": {
              "collection": "users",
              "dataSource": "main"
            },
            "properties": {
              "actions": {
                "type": "void",
                "x-component": "ActionBar"
              },
              "table": {
                "type": "array",
                "x-component": "TableV2"
              }
            }
          }
        }
      }
    }
  }'
```

### 폼 블록 생성
```bash
curl -X POST http://localhost:22001/api/uiSchemas \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4" \
  -H "Content-Type: application/json" \
  -d '{
    "type": "void",
    "x-component": "Grid.Row",
    "properties": {
      "form": {
        "type": "void",
        "x-component": "Grid.Col",
        "properties": {
          "form": {
            "type": "void",
            "x-decorator": "FormBlockProvider",
            "x-component": "CardItem",
            "x-decorator-props": {
              "collection": "users",
              "dataSource": "main"
            },
            "properties": {
              "form": {
                "type": "void",
                "x-component": "FormV2"
              }
            }
          }
        }
      }
    }
  }'
```

## 4. 컬렉션(테이블) 관리 API

### 컬렉션 생성
```bash
curl -X POST http://localhost:22001/api/collections \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "my_collection",
    "title": "My Collection"
  }'
```

### 컬렉션 조회
```bash
curl -X GET http://localhost:22001/api/collections \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4"
```

### 필드 추가
```bash
curl -X POST http://localhost:22001/api/collections/:name/fields \
  -H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VySWQiOjEsInJvbGVOYW1lIjoicm9vdCIsImlhdCI6MTc2MzUzNzQ4OSwiZXhwIjozMzMyMTEzNzQ4OX0.5gOLfD22RiswDcFECzkotidYeUae594fSpjdVBu_Sp4"
```

## 주요 컴포넌트

- `Menu.Item`: 메뉴 아이템
- `Page`: 페이지
- `Grid`, `Grid.Row`, `Grid.Col`: 레이아웃
- `TableBlockProvider`: 테이블 블록 제공자
- `FormBlockProvider`: 폼 블록 제공자
- `CardItem`: 카드 컨테이너
- `TableV2`: 테이블 컴포넌트
- `FormV2`: 폼 컴포넌트
- `ActionBar`: 액션 바

## 참고사항

1. 모든 API 호출에는 인증 토큰이 필요합니다
2. UI Schema는 JSON Schema 기반입니다
3. 각 블록은 Grid 레이아웃 시스템을 사용합니다
4. 컬렉션과 데이터소스를 먼저 설정해야 합니다
5. x-uid는 각 스키마의 고유 식별자입니다