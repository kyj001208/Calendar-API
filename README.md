# 캘린더 관리 애플리케이션

## 1. 프로젝트 설명

이 프로젝트는 Spring Boot를 기반으로 한 캘린더 일정 관리 애플리케이션입니다.  
사용자는 월별 또는 특정 날짜의 일정을 조회하고, 새로운 일정을 추가, 수정, 삭제할 수 있습니다.  
React.js 프론트엔드와 RESTful API로 통신하며, 데이터를 MySQL 데이터베이스에 저장합니다.


## 2. 소스 빌드 및 실행 방법

### 2.1. **필요 환경**
- Java 17.0.10
- Gradle 8.11.1
- MySQL 8.0.40
- Node.js (React 프론트엔드 실행용)

### 2.2. **백엔드 실행 방법**

1. **프로젝트 클론**
   ```bash
   git clone https://github.com/kyj001208/Calendar-API.git
   cd <프로젝트 폴더>
   
### 2.3 **MySQL 데이터베이스 설정**

**아래의 스키마를 생성합니다**
CREATE DATABASE calendar_db CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;

**기본 사용자와 비밀번호 설정(변경 시 application.properties에 반영)**
  
    spring.datasource.url: jdbc:mysql://localhost:3306/calendar_db
    
    spring.datasource.username: root
    
    spring.datasource.password: yourpassword

**백엔드 실행**

./gradlew bootRun
기본적으로 애플리케이션은 http://localhost:8080에서 실행됩니다.

### 3. 사용한 라이브러리와 이유

**Spring Boot**
사용 이유: 빠르고 효율적인 RESTful API 구축을 지원하며, 데이터베이스 연동과 비즈니스 로직을 간편하게 처리할 수 있습니다.

**Lombok**
사용 이유: 코드 간소화를 위해 Getter/Setter, Builder 패턴, Constructor 자동 생성을 활용.

**Hibernate/JPA**
사용 이유: 객체와 데이터베이스 간의 매핑을 효율적으로 관리하며, 데이터 접근 레이어를 간소화.

**MySQL**
사용 이유: 관계형 데이터베이스로 일정 관리에 적합하며, 안정적인 데이터 처리.

**Gradle**
사용 이유: 프로젝트 종속성을 효율적으로 관리하고, 빌드 속도가 빠름.


## 4. API 명세서

### API 상세

| 메서드   | 엔드포인트      | 설명                          | 요청 데이터          | 응답 데이터             |
|----------|-----------------|-------------------------------|----------------------|-------------------------|
| POST     | `/save`         | 일정 추가                     | `CalendarSaveDto`    | 저장 완료 메시지        |
| GET      | `/list`         | 월별 또는 특정 날짜 일정 조회 | `date`, `specificDay` | `List<CalendarListDto>` |
| PUT      | `/update/{id}`  | 일정 수정                     | `CalendarUpdateDto`  | 없음                    |
| DELETE   | `/delete/{id}`  | 일정 삭제                     | 없음                 | 없음                    |

## 5. 테스트케이스 작성

이 애플리케이션은 View(React.js 프론트엔드)에서 제공되는 UI를 통해 테스트할 수 있습니다.  
사용자는 브라우저를 통해 직접 일정을 추가, 조회, 수정, 삭제하며 API의 정상 동작 여부를 확인할 수 있습니다.

### 6.  테스트 방법
1. **애플리케이션 실행**  
   - 백엔드(Spring Boot) 실행:  
     ```bash
     ./gradlew bootRun
     ```
   - 프론트엔드(React.js) 실행:  
     ```bash
     npm start
     ```

2. **테스트 절차**
   - 브라우저에서 `http://localhost:3000`으로 이동합니다.
   - 제공된 UI에서 다음 기능을 테스트합니다:
     - **일정 추가**: 제목과 설명을 입력하여 새로운 일정 생성.
     - **일정 조회**: 월별 또는 특정 날짜에 저장된 일정 확인.
     - **일정 수정**: 기존 일정의 제목과 설명 변경.
     - **일정 삭제**: 불필요한 일정 삭제.

3. **테스트 결과 확인**
   - 일정 추가, 조회, 수정, 삭제가 정상적으로 동작하면, API 및 애플리케이션의 기본 기능이 올바르게 작동하고 있는 것입니다.

### 7.데이터베이스 스키마
**스키마 구조**

CREATE TABLE calendar (

    id BIGINT AUTO_INCREMENT PRIMARY KEY,
    
    title VARCHAR(255) ,
    
    description VARCHAR(255),
    
    selected_date DATE ,
    
    created_at TIMESTAMP ,
    
    updated_at TIMESTAMP
    
);

### 8. 프로젝트 목표
이 애플리케이션은 React.js와 Spring Boot를 활용하여 일정 관리 시스템을 구축하고, 데이터와 UI 간의 효율적인 상호작용을 학습하기 위해 제작되었습니다.MySQL 데이터베이스 설정
