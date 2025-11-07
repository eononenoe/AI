# AI

###  Git for Windows  설치
![git 다운로드 및 설치](https://git-scm.com/install/windows)

###  Node.js 설치
![Node.js 공식 사이트](https://nodejs.org/ko/download)에서 Windows 버전 다운로드(LTS 버전 권장)
```
node --version # v18이상
npm --version
```

### Claude Code 설치
Git Bash에서 다음 명령 실행 :
```
# Claude Code 전역 설치
npm install -g @anthropic-ai/claude-code

# 설치 확인
claude --version
```

###  모델 선택 명령어

```
// 모델 선택 방법들
# 실행 시 모델 지정
claude --model claude-opus-4-20250514
claude --model claude-sonnet-4-20250514

# 실행 중에 모델 변경
/model claude-opus-4
/model claude-sonnet-4

# 현재 모델 확인
/config

- 취소는 ctrl + c X / esc O
```

### 슬래시 명령어 vs 자연어

1) 자연어 명령 방식
```
ex) 코딩 작업 관련 요청
# 파일 생성/수정
package.json에 새로운 의존성을 추가해줘

# 코드 분석  
이 함수에서 성능 병목이 있는지 확인해줘

# 버그 수정
TypeError가 발생하는 이유를 찾아서 고쳐줘
```
2) 슬래시 명령어
```
2-1) 기본 세션 관리
/clear          # 대화 컨텍스트 초기화 (중요!)
/cost           # 현재 세션 토큰 사용량과 비용 확인
/status         # Claude Code 상태 (버전, 모델, 계정, API 연결 상태)
/help           # 사용 가능한 모든 슬래시 명령어 목록
```
```
2-2) 설정 및 환경
/init           # 프로젝트 초기 설정 (CLAUDE.md 자동 생성)
/terminal-setup # 터미널 키바인딩 설정 (Shift+Enter 등)
/claude-md      # 프로젝트 메모리 파일(CLAUDE.md) 생성
/config         # Claude Code 설정 보기/변경
/model          # 사용할 모델 변경 (Opus 4, Sonnet 4 등)
/permissions    # 권한 설정 관리

/status 살펴보면 memory라는 항목이 따로있다 
이때 CLAUDE.md 파일을 보면 프로젝트를 이해하는데 사용하는 "메모리" 역할을 한다.
```
```
// CLAUDE.md 생성
/claude-md

# 또는 직접 요청
이 프로젝트에 대한 정보를 CLAUDE.md 파일로 만들어줘:
- 기술 스택
- 프로젝트 구조  
- 코딩 컨벤션
- 중요한 설정들

CLAUDE.md 장점프로젝트 루트에 CLAUDE.md가 있으면 매번 컨텍스트를 설명할 필요가 없다. 팀원들과 공유해서 모든 사람이 같은 컨텍스트로 Claude Code를 사용할 수 있다.
```
```
2-3) 개발 도구
/install-github-app  # GitHub PR 자동 리뷰 설정
/bug                 # 버그 리포트 전송
/diff                # Git diff 보기
/commit              # Git 커밋 생성
/compact             # 대화 기록 요약 후 보존
/clear               # 대화 기록 완전 삭제
```

## 작업모드 3가지
Claude Code는 상황에 맞게 선택할 수 있는 3가지 작업 모드를 제공한다.

| 모드 | 특징 | 적합한 상황 |
|------|------|-------------|
| 기본 모드 | 매번 승인 후 파일 수정 | 신중한 작업, 처음 사용할 때 |
| 자동 승인 | 자동으로 파일 수정 | 반복 작업, 신뢰할 때 |
| 플랜 모드 | 코드 작성 전 계획 제안 | 복잡한 작업, 설계 단계 |
```
// 모드 전환
# Shift+Tab으로 모드 전환
# 또는 직접 지정
claude --mode auto    # 자동 승인 모드
claude --mode plan    # 플랜 모드

```

## 파일 참조 방법
```
// 다양한 참조 방법들
# @ 기호로 파일 참조
@src/components/UserList.jsx에서 로딩 상태를 추가해줘

# # 기호로 프로젝트 컨텍스트 실시간 추가
# 이 프로젝트는 React 18 + TypeScript를 사용합니다

# URL로 웹 컨텐츠 참조
https://docs.react.dev/learn 이 문서를 참고해서 Hook을 설명해줘

# 여러 파일 동시 참조
@package.json과 @tsconfig.json을 보고 TypeScript 설정을 최적화해줘

# 디렉토리 전체 참조  
@src/utils/ 폴더의 모든 함수에 JSDoc 주석을 추가해줘
```
> 이미지도 참조 가능  
> Shift + 드래그 로 이미지 파일을 터미널에 직접 첨부할 수 있다.  
> Claude가 이미지를 분석해서 코드 컨텍스트로 활용한다.  
> UI 디자인을 보고 컴포넌트를 만들어달라고 할 때 유용하다.

## 새 기능 개발하기
```
기능 요구사항을 자연어로 설명하면 알아서 구현 한다
- 기능 개발 예시
# 간단한 API 개발
사용자 로그인 API를 만들어줘. JWT 토큰 사용하고, 
비밀번호는 bcrypt로 해싱해서 저장하고, 
실패 시 적절한 에러 메시지 반환하도록

# 복잡한 기능 개발
게시판 CRUD API를 Express.js로 만들고, 
MongoDB 연동하고, 파일 업로드 기능도 추가해줘. 
테스트 코드도 같이 작성해줘
```

## 응용? 활용버전
```
GitHub PR 자동 리뷰 
 - GitHub 앱을 설치하면 PR을 올릴 때마다 Claude가 자동으로 리뷰해주는 기능

개발 도구
/install-github-app  # GitHub PR 자동 리뷰 설정
/bug                 # 버그 리포트 전송
/diff                # Git diff 보기
/commit              # Git 커밋 생성

// GitHub 자동 리뷰 설정
/install-github-app

# 설정 완료 후 자동으로 생성되는 파일
# .github/claude-code-review.yml
```
```
 리뷰 프롬프트 커스터마이징
# claude-code-review.yml 예시
prompt: |
  이 PR을 리뷰해줘. 다음에 집중해줘:
  - 보안 취약점
  - 성능 이슈
  - 버그 가능성
  - 코드 품질 개선점
  
  변수명이나 사소한 스타일은 신경쓰지 말고,
  실제 문제가 될 수 있는 것들만 간결하게 알려줘.
```

## 실시간 로그 모니터링
```
Unix 파이프라인과 연동해서 실시간 로그 모니터링도 가능하다
// 로그 실시간 분석
# 에러 발생 시 슬랙 알림
tail -f /var/log/app.log | claude -p "에러나 warn이 나오면 슬랙으로 알려줘"

# 성능 지표 모니터링
kubectl logs -f deployment/my-app | claude -p "응답시간이 1초 넘으면 알려줘"

# 배포 로그 분석
docker logs -f container_name | claude -p "배포 관련 이슈가 있으면 정리해서 알려줘"
```

## 연속 작업 큐와 대화 제어
```
Claude Code는 여러 작업을 효육적으로 처리할 수 있는 고급 기능들을 제공한다
작업 큐 관리

순차 실행 : 여러 메시지를 연속으로 입력하면 큐에 쌓여서 순차적으로 처리됨
작업 중단 : Escape 키로 현재 작업 중단 (많이 사용한다. ctrl or command + c가 아니다.)
대화 분기 : Escape 두 번으로 이전 메시지로 돌아가서 다른 방향으로 진행
```
```
// 연속 작업 예시
# 여러 작업을 한 번에 요청
1. package.json에 새 의존성 추가해줘
2. 그 다음에 컴포넌트 생성해줘  
3. 마지막으로 테스트 파일도 만들어줘

# Claude가 순차적으로 처리
# 중간에 문제가 생기면 Escape로 중단 가능
```

## 대화 세션 연결과 재개
```
장기 프로젝트, 특정 기간동안 개발하던 세션 관련 유용한 기능

// 세션 연결 명령어들
# 가장 최근 세션 이어받기
claude --continue

# 특정 세션 목록 확인하여 선택 이어받기
claude --resume

# 스크립트 내에서 이어받기 예시
claude --continue -p "continue working on the code review"
```

## 사용자 정의 커맨드 만들기
```
반복되는 작업을 자동화하기 위해 나만의 슬래시 커맨드를 만들 수 있다.
공식 문서 : https://github.com/qdhenry/Claude-Command-Suite

커스텀 커맨드 생성 과정

프로젝트 루트에 .claude/commands/ 폴더 생성
마크다운 파일로 커맨드 정의 (예: cleanup.md)
/cleanup 형태로 사용
```
```
커맨드 파일 예시
# .claude/commands/cleanup.md
코드를 다음 기준으로 정리해줘:
- 사용하지 않는 import 제거
- 콘솔 로그 삭제  
- 일관된 들여쓰기 적용
- ESLint 규칙 준수

# .claude/commands/review.md  
다음 관점에서 코드를 리뷰해줘:
- 보안 취약점
- 성능 이슈
- 버그 가능성
- 코드 품질

# .claude/commands/explain.md
이 코드를 초보 개발자도 이해할 수 있게 설명해줘:
- 각 함수의 역할
- 데이터 흐름
- 주요 로직
```
```
// 커스텀 커맨드 사용 예시
# 사용자 정의 커맨드 실행
/cleanup @src/components/TestComponent.jsx
/review @src/api/appcard.js  
- 리뷰
/explain @utils/testUtil.js
- 설명요청

# 매개변수와 함께 사용
/deploy staging
/test unit
```

## VS Code/Cursor 확장 프로그램 연동
```
터미널 작업이 불편하다면 IDE 확장 프로그램으로 더 편리하게 사용할 수 있다:

지원하는 IDE들
VS Code : 공식 확장 프로그램 지원
Cursor : 확장 프로그램으로 IDE 내에서 직접 사용
Windsurf : VS Code 기반이라 호환 가능
JetBrains : IntelliJ, PyCharm, WebStorm 등 지원
```
```
// IDE 확장 기능들
# 빠른 실행 단축키
Cmd+Esc (Mac) / Ctrl+Esc (Windows/Linux)

# 파일 참조 단축키  
Cmd+Option+K (Mac) / Alt+Ctrl+K (Windows/Linux)

# IDE 터미널에서 실행
claude

# 외부 터미널에서 IDE 연결
/ide
```
```
 IDE 확장의 장점

Interactive Diff: 코드 변경사항을 IDE 내 diff 뷰어로 확인
Selection Context: 현재 선택한 코드가 자동으로 컨텍스트에 포함
Diagnostic Sharing: 린트 에러나 문법 오류가 자동으로 공유
Multiple Instances: 여러 Claude Code 인스턴스를 다른 패널에서 동시 실행
```

## MCP
```
Model Context Protocol(MCP)를 통해 다양한 외부 도구와 연동할 수 있다.
mcp는 너무 중요하니 별도로 진행하고 간단히 예시만 확인.

지원하는 MCP 서버들
Google Drive: 설계 문서나 요구사항 읽기
Slack: 팀 커뮤니케이션 자동화
Jira: 이슈 생성/업데이트
Figma: 디자인 스펙 확인
Sentry: 에러 트래킹
Puppeteer: 웹 자동화
```
```
// MCP 서버 설정 예시
# .mcp.json 파일 생성
{
  "mcpServers": {
    "google-drive": {
      "command": "npx",
      "args": ["@google-drive/mcp-server"],
      "env": {"GOOGLE_APPLICATION_CREDENTIALS": "./credentials.json"}
    },
    "slack": {
      "command": "npx", 
      "args": ["@slack/mcp-server"],
      "env": {"SLACK_BOT_TOKEN": "xoxb-your-token"}
    }
  }
}
```

## 터미널
```
키보드 단축키

Shift+Tab: 작업 모드 전환 (기본 ↔ 자동 ↔ 플랜)
Escape: Claude 작업 중단 (Ctrl+C가 아니다)
Escape x2: 이전 메시지로 대화 분기
↑ 화살표: 이전 세션 탐색
```

## 성능 최적화
| 상황 | 권장사항 | 이유 |
|------|-----------|------|
| 새 작업 시작 | `/clear` 실행 | 컨텍스트 정리, 토큰 절약 |
| 복잡한 작업 | Opus 4 사용 | 더 나은 추론 능력 |
| 간단한 작업 | Sonnet 4 사용 | 비용 절약 |
| 대용량 파일 | `@파일명`으로 참조 | 선택적 컨텍스트 포함 |
```
 최고의 활용법18,000줄짜리 React 컴포넌트도 Claude Code는 문제없이 수정한다. Cursor 같은 다른 도구들이 헤맬 때도 Claude Code는 안정적으로 동작한다. 큰 파일이나 복잡한 작업일수록 Claude Code의 장점이 드러난다.
```

## 비용 관리
Claude Code는 API 요금을 사용하므로 비용을 주의깊게 관리해야 한다:
```
// 비용 모니터링
/cost                    # 현재 세션 비용 확인
ccusage                  # 전체 사용량 분석 (별도 설치)

# 비용 절약 팁
/clear                   # 불필요한 컨텍스트 정리
/model claude-sonnet-4   # 저렴한 모델 사용
```