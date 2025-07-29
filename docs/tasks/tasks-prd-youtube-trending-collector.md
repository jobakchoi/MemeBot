# 작업 목록: 유튜브 음악 '이번주 베스트' 영상 수집 슬랙봇

**PRD 참조:** `docs/prd/active/prd-youtube-trending-collector.md`

## 관련 파일

- `src/main/java/com/jobakchoi/memebot/entity/MusicBestVideo.java` - 유튜브 음악 '이번주 베스트' 영상 정보를 저장하는 JPA 엔티티
- `src/main/java/com/jobakchoi/memebot/entity/MusicBestVideoRepository.java` - 데이터베이스 접근을 위한 JPA Repository
- `src/main/java/com/jobakchoi/memebot/entity/SlackAlert.java` - 슬랙 알림 설정 정보를 저장하는 JPA 엔티티
- `src/main/java/com/jobakchoi/memebot/entity/SlackAlertRepository.java` - 슬랙 알림 설정 데이터베이스 접근
- `src/main/java/com/jobakchoi/memebot/service/YoutubeMusicBestScraperService.java` - 유튜브 음악 '이번주 베스트' 데이터 수집 서비스
- `src/main/java/com/jobakchoi/memebot/service/MusicBestDataCollectorService.java` - 음악 베스트 데이터 수집 및 처리 서비스
- `src/main/java/com/jobakchoi/memebot/service/SlackNotificationService.java` - 슬랙 알림 전송 서비스
- `src/main/java/com/jobakchoi/memebot/service/SlackMessageFormatter.java` - 슬랙 메시지 포맷팅 서비스
- `src/main/java/com/jobakchoi/memebot/service/SlackAlertManager.java` - 슬랙 알림 설정 관리 서비스
- `src/main/java/com/jobakchoi/memebot/scheduler/MusicBestDataScheduler.java` - 스케줄링 작업 관리
- `src/main/java/com/jobakchoi/memebot/controller/SlackBotController.java` - 슬랙봇 컨트롤러
- `src/main/java/com/jobakchoi/memebot/handler/SlackCommandHandler.java` - 슬랙 명령어 처리기
- `src/main/java/com/jobakchoi/memebot/dto/MusicBestVideoDto.java` - 데이터 전송 객체
- `src/main/java/com/jobakchoi/memebot/config/SlackConfig.java` - 슬랙 설정 클래스
- `src/main/resources/db/migration/V1__create_music_best_video_table.sql` - 데이터베이스 마이그레이션 파일
- `src/main/resources/db/migration/V2__create_slack_alert_table.sql` - 슬랙 알림 설정 테이블 마이그레이션
- `src/test/java/com/jobakchoi/memebot/service/YoutubeMusicBestScraperServiceTest.java` - 유튜브 음악 베스트 스크래퍼 서비스 단위 테스트
- `src/test/java/com/jobakchoi/memebot/service/MusicBestDataCollectorServiceTest.java` - 음악 베스트 데이터 수집 서비스 단위 테스트
- `src/test/java/com/jobakchoi/memebot/service/SlackNotificationServiceTest.java` - 슬랙 알림 서비스 단위 테스트
- `src/test/java/com/jobakchoi/memebot/handler/SlackCommandHandlerTest.java` - 슬랙 명령어 처리기 단위 테스트

### 메모

- 단위 테스트는 일반적으로 테스트 대상 클래스와 같은 패키지 구조로 test 디렉토리에 배치합니다.
- 테스트 실행은 `./gradlew test` 또는 `gradle test` 명령어로 진행합니다.
- 웹 스크래핑을 위해 Selenium 또는 Jsoup 의존성을 build.gradle.kts에 추가해야 합니다.
- 슬랙봇 구현을 위해 Slack SDK for Java 의존성을 추가해야 합니다.
- 슬랙 앱 설정에서 Slash Commands와 Incoming Webhooks 권한을 설정해야 합니다.
- 슬랙 토큰과 시크릿은 환경 변수나 application.properties에서 관리해야 합니다.

## Tasks

- [ ] 1.0 데이터 모델 및 데이터베이스 설계
  - [ ] 1.1 MusicBestVideo 엔티티 클래스 생성 (날짜, 제목, 채널명, 순위, URL, 조회수, 게시일 필드)
  - [ ] 1.2 MusicBestVideoRepository 인터페이스 생성 (날짜별 조회, 채널별 조회 메서드 포함)
  - [ ] 1.3 SlackAlert 엔티티 클래스 생성 (채널명, 슬랙 채널 ID, 알림 설정 필드)
  - [ ] 1.4 SlackAlertRepository 인터페이스 생성 (알림 설정 관리 메서드 포함)
  - [ ] 1.5 데이터베이스 마이그레이션 스크립트 작성 (MusicBestVideo 테이블)
  - [ ] 1.6 슬랙 알림 설정 마이그레이션 스크립트 작성 (SlackAlert 테이블)
  - [ ] 1.7 데이터베이스 연결 설정 (application.properties 수정)
  - [ ] 1.8 MusicBestVideoDto 클래스 생성 (슬랙 메시지용)

- [ ] 2.0 유튜브 음악 베스트 데이터 수집 시스템 구현
  - [ ] 2.1 웹 스크래핑 라이브러리 의존성 추가 (Selenium 또는 Jsoup)
  - [ ] 2.2 YoutubeMusicBestScraperService 클래스 생성 ('음악' 카테고리 '이번주 베스트' 스크래핑)
  - [ ] 2.3 쇼츠 필터링 로직 구현 (URL 형식 분석)
  - [ ] 2.4 영상 정보 파싱 로직 구현 (제목, 채널명, 조회수, 게시일 추출)
  - [ ] 2.5 상위 10개 영상 필터링 로직 구현
  - [ ] 2.6 MusicBestDataCollectorService 클래스 생성 (수집된 데이터 처리 및 저장)
  - [ ] 2.7 중복 데이터 방지 로직 구현

- [ ] 3.0 스케줄링 및 자동화 구현
  - [ ] 3.1 MusicBestDataScheduler 클래스 생성 (@Scheduled 어노테이션 활용)
  - [ ] 3.2 매일 '음악' 카테고리 '이번주 베스트' 데이터 수집 스케줄 설정
  - [ ] 3.3 매주 월요일 오전 11시 30분 슬랙 리포트 전송 스케줄 설정
  - [ ] 3.4 데이터 수집 실패 시 재시도 로직 구현 (최대 3회)
  - [ ] 3.5 오류 로깅 시스템 구현 (SLF4J + Logback)
  - [ ] 3.6 부분적 데이터 수집 실패 처리 로직 구현
  - [ ] 3.7 스케줄러 활성화 설정 (@EnableScheduling)
  - [ ] 3.8 실시간 알림 체크 로직 구현 (새로운 채널 진입 감지)

- [ ] 4.0 슬랙봇 명령어 및 알림 기능 구현
  - [ ] 4.1 SlackConfig 클래스 생성 (슬랙 토큰 및 설정 관리)
  - [ ] 4.2 SlackBotController 클래스 생성 (슬랙 이벤트 처리)
  - [ ] 4.3 SlackCommandHandler 클래스 생성 (명령어 라우팅)
  - [ ] 4.4 /music-best 명령어 핸들러 구현 (오늘의 음악 베스트 조회)
  - [ ] 4.5 /music-best-channel 명령어 핸들러 구현 (채널별 이력 조회)
  - [ ] 4.6 /music-best-stats 명령어 핸들러 구현 (통계 조회)
  - [ ] 4.7 /music-best-history 명령어 핸들러 구현 (특정 날짜 조회)
  - [ ] 4.8 /music-best-alert 명령어 핸들러 구현 (알림 설정)
  - [ ] 4.9 SlackNotificationService 클래스 생성 (알림 전송)

- [ ] 5.0 슬랙 메시지 포맷팅 및 통계 분석 기능 구현
  - [ ] 5.1 SlackMessageFormatter 클래스 생성 (메시지 포맷팅)
  - [ ] 5.2 음악 베스트 영상 리스트 메시지 포맷 구현
  - [ ] 5.3 채널별 순위 변화 텍스트 포맷 구현
  - [ ] 5.4 일별, 주별, 월별 음악 트렌드 통계 분석 로직 구현
  - [ ] 5.5 채널별 음악 베스트 진입 횟수 통계 구현
  - [ ] 5.6 SlackAlertManager 클래스 생성 (알림 설정 관리)
  - [ ] 5.7 실시간 채널 진입 감지 및 알림 로직 구현
  - [ ] 5.8 슬랙 블록 킷을 활용한 리치 메시지 구현
  - [ ] 5.9 에러 메시지 포맷팅 및 관리자 알림 구현

- [ ] 6.0 슬랙봇 배포 및 설정
  - [ ] 6.1 Slack SDK for Java 의존성 추가 (build.gradle.kts)
  - [ ] 6.2 슬랙 앱 생성 및 권한 설정 (Slash Commands, Incoming Webhooks)
  - [ ] 6.3 application.properties에 슬랙 토큰 및 설정 추가
  - [ ] 6.4 슬랙 앱 Event Subscriptions 설정
  - [ ] 6.5 슬랙 앱 OAuth & Permissions 설정
  - [ ] 6.6 슬랙 워크스페이스에 봇 설치 및 테스트
  - [ ] 6.7 슬랙 명령어 URL 엔드포인트 설정
  - [ ] 6.8 프로덕션 환경 배포 및 설정

---

**생성일:** 2025년 7월 15일  
**상태:** 진행 중 