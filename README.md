# MemeBot

## 기술 스택

### 백엔드
- **Language**: Java 17
- **Framework**: Spring Boot 3.3.5
- **Build Tool**: Gradle (Kotlin DSL)

### 주요 의존성
#### Spring Boot Starters
- Spring Boot Batch
- Spring Boot Data JPA
- Spring Boot Validation

#### Database
- MySQL

#### 개발 도구
- Lombok - 자바 코드 생성 라이브러리
- JUnit - 테스트 프레임워크

### 개발 환경
- Java 17
- Spring Boot 3.3.5
- Gradle 사용 (Kotlin DSL)
- MySQL Database

## 프로젝트 구조
```
.
├── src/                    # 소스 코드
├── gradle/                 # Gradle Wrapper 설정
├── build.gradle.kts        # Gradle 빌드 설정
├── settings.gradle.kts     # Gradle 프로젝트 설정
└── README.md              # 프로젝트 문서
```

## 주요 기능
- Spring Batch를 활용한 배치 처리
- JPA를 이용한 데이터베이스 연동
- 데이터 유효성 검증 (Validation) 