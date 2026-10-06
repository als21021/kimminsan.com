# kimminsan.com

Hugo 정적 사이트. 외부 테마 없이 layouts/와 assets/만으로 구성한다.
GitHub push 시 Cloudflare Workers(kimminsan-com)가 빌드·배포한다.

## 목적
임베디드 직군 지원용 포트폴리오 + 기술 블로그. 언어는 한국어.

## 페이지
- 홈: 이름, 한 줄 소개(임베디드 · C/C++ · STM32), GitHub/메일 링크, featured 프로젝트 카드, 최근 글 5개
- /projects/: 프로젝트 카드 그리드, 개별 페이지
- /posts/: 날짜순 글 목록, 개별 페이지(목차, 코드 하이라이팅)
- /about/: 이력, 기술 스택
- 404 페이지, RSS, sitemap

## 프로젝트 front matter
title, date, summary, tech(배열), board, github, featured(bool), cover(선택)
archetypes/projects.md 로 템플릿 제공할 것.

## 디자인 규칙
- JS 프레임워크 금지. 필요하면 바닐라 JS 최소한으로(다크모드 토글 정도)
- CSS는 assets/css/main.css 하나, Hugo Pipes로 minify + fingerprint
- 폰트: Pretendard(본문), 코드는 monospace 시스템 폰트
- 다크모드: prefers-color-scheme 기본 + 수동 토글, 색은 CSS 변수로
- 반응형, word-break: keep-all
- 코드 하이라이팅은 Hugo 내장 Chroma(noClasses = false, CSS 생성)

## 작업 규칙
- 변경 후 반드시 `hugo --gc --minify`로 빌드 에러 확인
- partial로 header/footer/card 분리, 중복 템플릿 금지

## 구현 메모
- 템플릿은 Hugo 0.146+ 구조: layouts/{baseof,home,list,single,404}.html, layouts/_partials/, 섹션 전용은 layouts/projects/
- Chroma CSS는 main.css 맨 아래에 있다. 스타일을 바꾸려면 `hugo gen chromastyles --style=<이름>` 출력을
  라이트는 `:root:not([data-theme="dark"])`, 다크는 `[data-theme="dark"]` 접두사로 감싸 교체한다(섞이면 색이 샌다)
- timeZone = Asia/Seoul. 시간 없는 date가 UTC로 해석돼 '미래 글'로 빠지는 것을 막는다
- 프로젝트 cover 이미지는 페이지 번들(content/projects/<slug>/) 안에 둔다
