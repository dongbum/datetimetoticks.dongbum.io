# CLAUDE.md — DateTime Ticks Converter

## 프로젝트 개요

- **URL**: https://datetimetoticks.dongbum.io/
- **GitHub**: https://github.com/dongbum/datetimetoticks.dongbum.io
- **구조**: 빌드 도구 없는 단일 정적 HTML (`index.html` 하나가 전부)
- **배포**: Netlify (push → 자동 배포), 배포 시 IndexNow로 검색엔진에 URL 제출

## 파일 구조

```
index.html          # 메인 페이지 (유일한 소스 파일)
sitemap.xml         # 검색엔진 사이트맵
robots.txt          # 크롤러 허용 설정
netlify.toml        # Netlify 빌드/배포 설정 + IndexNow 호출
favicon.ico         # 브라우저 탭 아이콘 (16/32/48px 멀티사이즈)
favicon-16x16.png
favicon-32x32.png
apple-touch-icon.png  # iOS 홈화면 아이콘 (180x180)
og-image.png        # SNS 공유 이미지 (1200x630)
images/             # 원본 이미지 보관 폴더
naverb8f55d0a127c4a8c915399be9f02a445.html  # 네이버 사이트 인증 파일
9008f07740eb64ffb5f879db3f3056eb.txt        # IndexNow 키 파일
```

## 주요 코드 / 키

| 항목 | 값 |
|------|-----|
| Google Analytics ID | `G-JZNE7QPDSC` |
| AdSense Publisher ID | `ca-pub-6818401304157689` |
| AdSense Ad Slot | `3514324891` |
| IndexNow Key | `9008f07740eb64ffb5f879db3f3056eb` |

## 다국어 지원 구조

- **감지 방식**: `navigator.language`로 브라우저 언어 자동 감지
- **지원 언어**: 한국어(`ko`), 영어(`en`), 일본어(`ja`)
- **우선순위**: `ko` → 한국어, `ja` → 일본어, **그 외 모든 언어 → 영어**
- **초기 HTML**: 영어로 작성 → 검색엔진이 영어로 인덱싱
- **번역 객체**: `index.html` 내 `LANGS` 상수에서 관리
- **번역 대상 요소**: `#converterHeading`, `#labelDt`, `#labelTick`, `#tickInput`(placeholder), `#note`, `#infoHeading`, `#infoP1`, `#infoP2`, `#themeToggle`
- **`html[lang]` 속성**도 감지된 언어로 동적 변경

### 번역 텍스트 수정 시 주의사항

번역 텍스트를 추가하거나 수정할 때는 반드시 `LANGS` 객체의 **ko / en / ja 세 언어 모두** 수정해야 한다. 초기 HTML 본문의 영어 텍스트도 함께 수정해야 한다.

## AdSense 구조

- **`<script async src="...adsbygoogle.js">`**: `<head>` 안에 위치 (Google 권장)
- **`<ins>` 태그 + push 스크립트**: `</body>` 직전에 위치
- 두 섹션이 분리된 것은 정상이며 중복이 아님

## Google Analytics vs AdSense 구분

- `<!-- Google tag (gtag.js) -->`: Google Analytics (`googletagmanager.com`) — 방문자 분석
- `<!-- datetimetoticks.dongbum.io -->`: Google AdSense (`pagead2.googlesyndication.com`) — 광고

## SEO 설정 현황

- `<meta name="description">`: 한국어 (변경 시 영어로도 고려)
- Open Graph / Twitter Card: 영어 title, og:image 설정 완료
- JSON-LD: `WebApplication` 스키마, `inLanguage: ["ko","en","ja"]`
- `sitemap.xml`: 배포 후 `lastmod` 날짜 갱신 필요
- `robots.txt`: 전체 허용, sitemap URL 명시

## 아이콘 출처

| 항목 | 내용 |
|------|------|
| 원본 파일 | `images/alarm_1715050.png` |
| 출처 URL | https://www.magnific.com/icon/alarm_1715050#fromView=keyword&page=1&position=83 |
| 용도 | favicon, apple-touch-icon, og-image 생성에 사용 |

## 작업 규칙

1. **항상 새 브랜치 → PR → 머지 순서**로 작업한다. main에 직접 커밋하지 않는다.
2. PR 머지 후에는 로컬/원격 feature 브랜치를 모두 삭제한다.
3. `sitemap.xml`의 `lastmod`는 변경사항 배포 시마다 오늘 날짜로 갱신한다.
4. 이미지 원본은 `images/` 폴더에 보관한다.
5. favicon / og-image는 PowerShell + `System.Drawing`으로 생성한다.
