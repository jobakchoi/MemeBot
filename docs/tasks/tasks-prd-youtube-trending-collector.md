# 작업 목록: 유튜브 인기급상승 영상 순위 수집 기능

**PRD 참조:** `docs/prd/active/prd-youtube-trending-collector.md`

## 관련 파일

- `src/main/java/com/jobakchoi/memebot/entity/TrendingVideo.java` - 유튜브 영상 정보를 저장하는 JPA 엔티티
- `src/main/java/com/jobakchoi/memebot/entity/TrendingVideoRepository.java` - 데이터베이스 접근을 위한 JPA Repository
- `src/main/java/com/jobakchoi/memebot/service/YoutubeScraperService.java` - 유튜브 데이터 수집 서비스
- `src/main/java/com/jobakchoi/memebot/service/TrendingDataCollectorService.java` - 트렌드 데이터 수집 및 처리 서비스
- `src/main/java/com/jobakchoi/memebot/scheduler/TrendingDataScheduler.java` - 스케줄링 작업 관리
- `src/main/java/com/jobakchoi/memebot/controller/TrendingController.java` - REST API 컨트롤러
- `src/main/java/com/jobakchoi/memebot/dto/TrendingVideoDto.java` - 데이터 전송 객체
- `src/main/resources/static/js/trending-dashboard.js` - 대시보드 JavaScript 파일
- `src/main/resources/static/css/trending-dashboard.css` - 대시보드 스타일 파일
- `src/main/resources/templates/trending-dashboard.html` - 대시보드 Thymeleaf 템플릿
- `src/main/resources/db/migration/V1__create_trending_video_table.sql` - 데이터베이스 마이그레이션 파일
- `src/test/java/com/jobakchoi/memebot/service/YoutubeScraperServiceTest.java` - 유튜브 스크래퍼 서비스 단위 테스트
- `src/test/java/com/jobakchoi/memebot/service/TrendingDataCollectorServiceTest.java` - 트렌드 데이터 수집 서비스 단위 테스트

### 메모

- 단위 테스트는 일반적으로 테스트 대상 클래스와 같은 패키지 구조로 test 디렉토리에 배치합니다.
- 테스트 실행은 `./gradlew test` 또는 `gradle test` 명령어로 진행합니다.
- 웹 스크래핑을 위해 Selenium 또는 Jsoup 의존성을 build.gradle.kts에 추가해야 합니다.

## Tasks

- [ ] 1.0 데이터 모델 및 데이터베이스 설계
  - [ ] 1.1 TrendingVideo 엔티티 클래스 생성 (날짜, 제목, 채널명, 순위, URL, 조회수, 게시일 필드)
  - [ ] 1.2 TrendingVideoRepository 인터페이스 생성 (날짜별 조회, 채널별 조회 메서드 포함)
  - [ ] 1.3 데이터베이스 마이그레이션 스크립트 작성
  - [ ] 1.4 데이터베이스 연결 설정 (application.properties 수정)
  - [ ] 1.5 TrendingVideoDto 클래스 생성 (API 응답용)

- [ ] 2.0 유튜브 데이터 수집 시스템 구현
  - [ ] 2.1 웹 스크래핑 라이브러리 의존성 추가 (Selenium 또는 Jsoup)
  - [ ] 2.2 YoutubeScraperService 클래스 생성 (유튜브 트렌딩 페이지 스크래핑)
  - [ ] 2.3 쇼츠 필터링 로직 구현 (URL 형식 분석)
  - [ ] 2.4 영상 정보 파싱 로직 구현 (제목, 채널명, 조회수, 게시일 추출)
  - [ ] 2.5 상위 20개 영상 필터링 로직 구현
  - [ ] 2.6 TrendingDataCollectorService 클래스 생성 (수집된 데이터 처리 및 저장)
  - [ ] 2.7 중복 데이터 방지 로직 구현

- [ ] 3.0 스케줄링 및 자동화 구현
  - [ ] 3.1 TrendingDataScheduler 클래스 생성 (@Scheduled 어노테이션 활용)
  - [ ] 3.2 매일 오전 11시 실행 스케줄 설정
  - [ ] 3.3 데이터 수집 실패 시 재시도 로직 구현 (최대 3회)
  - [ ] 3.4 오류 로깅 시스템 구현 (SLF4J + Logback)
  - [ ] 3.5 부분적 데이터 수집 실패 처리 로직 구현
  - [ ] 3.6 스케줄러 활성화 설정 (@EnableScheduling)

- [ ] 4.0 웹 인터페이스 및 대시보드 구현
  - [ ] 4.1 TrendingController REST API 구현 (날짜별 데이터 조회 엔드포인트)
  - [ ] 4.2 채널별 데이터 조회 API 구현
  - [ ] 4.3 통계 데이터 조회 API 구현
  - [ ] 4.4 대시보드 HTML 템플릿 생성 (Thymeleaf)
  - [ ] 4.5 대시보드 CSS 스타일 작성
  - [ ] 4.6 대시보드 JavaScript 로직 구현 (AJAX 호출)
  - [ ] 4.7 날짜 범위 필터링 기능 구현
  - [ ] 4.8 채널별 필터링 기능 구현
  - [ ] 4.9 반응형 디자인 적용

- [ ] 5.0 데이터 분석 및 시각화 기능 구현
  - [ ] 5.1 Chart.js 라이브러리 통합
  - [ ] 5.2 순위 변화 라인 차트 구현
  - [ ] 5.3 채널별 순위 변화 추이 차트 구현
  - [ ] 5.4 일별, 주별, 월별 트렌드 분석 API 구현
  - [ ] 5.5 채널별 인기급상승 진입 횟수 통계 구현
  - [ ] 5.6 기본 통계 데이터 생성 기능 구현
  - [ ] 5.7 대시보드에 시각화 컴포넌트 통합
  - [ ] 5.8 데이터 내보내기 기능 구현 (선택사항)

---

**생성일:** 2025년 7월 15일  
**상태:** 진행 중 