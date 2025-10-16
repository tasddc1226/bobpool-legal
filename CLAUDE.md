# CLAUDE.md

이 파일은 이 저장소에서 작업할 때 Claude Code (claude.ai/code)에게 제공되는 가이드입니다.

## 프로젝트 개요

BobPool 법적 문서 웹사이트 - BobPool 레시피 공유 모바일 앱을 위한 법적 문서(개인정보처리방침 및 이용약관)를 호스팅하는 정적 웹사이트. GitHub Pages를 통해 커스텀 도메인 `legal.bobpool.app`으로 배포됨.

**목적**: 앱 스토어 요구사항(Apple App Store, Google Play Store) 충족 및 한국 법률 준수(개인정보보호법, 전자상거래법, 정보통신망법).

**기술 스택**: 정적 HTML/CSS/JS, GitHub Pages, PWA 호환

## 핵심 명령어

### 배포
```bash
# GitHub Actions를 통한 자동 배포 (main 브랜치에 푸시 시)
git add .
git commit -m "Update legal documents"
git push origin main

# 수동 Pages 배포 트리거
# GitHub Actions 워크플로우: .github/workflows/deploy.yml
```

**중요**: GitHub Actions 워크플로우가 `./legal-website` 경로를 참조하지만 파일들은 루트에 있음. 필요시 워크플로우 경로를 `'.'`로 업데이트해야 함.

### 검증
```bash
# HTML 유효성 테스트 (html validator 설치 시)
html5validator --root . --ignore CNAME --ignore README.md

# 링크 확인
# 배포 후 모든 내부/외부 링크가 작동하는지 수동으로 확인

# 모바일 반응형 테스트
# 브라우저 DevTools 반응형 모드 또는 실제 디바이스에서 테스트
```

### 로컬 개발
```bash
# Python으로 로컬 서버 실행
python3 -m http.server 8000

# 또는 Node.js로 실행
npx serve .

# 그 후 http://localhost:8000 열기
```

## 아키텍처 및 구조

### 파일 구조
```
.
├── index.html                    # 다국어 지원 랜딩 페이지
├── privacy-policy.html           # 한국어 개인정보처리방침
├── privacy-policy-en.html        # 영어 개인정보처리방침
├── terms-of-service.html         # 한국어 이용약관
├── terms-of-service-en.html      # 영어 이용약관
├── signup-complete.html          # 회원가입 완료 확인 페이지
├── privacy-policy-ko.md          # 소스 마크다운 (한국어)
├── terms-of-service-ko.md        # 소스 마크다운 (한국어)
├── manifest.json                 # PWA 매니페스트
├── robots.txt                    # SEO
├── sitemap.xml                   # SEO
├── CNAME                         # GitHub Pages 커스텀 도메인 설정
└── .github/workflows/deploy.yml  # 자동 배포
```

### 디자인 시스템

**CSS 아키텍처**:
- 테마 일관성을 위한 `:root`의 CSS 변수
- 모바일 우선 반응형 디자인
- 성능을 위한 인라인 CSS (HTTP 요청 제거)
- 디자인 토큰:
  - Primary: `#4CAF50` (녹색)
  - Secondary: `#2E7D32` (진한 녹색)
  - Accent: `#FF9800` (주황색)

**주요 기능**:
- WCAG 2.1 AA 접근성 준수
- localStorage 지속성이 있는 한국어/영어 언어 전환
- 시맨틱 HTML5 구조
- 스크린 리더용 콘텐츠 건너뛰기 링크
- 가독성을 위한 고대비 색상

### JavaScript 기능

**언어 전환 시스템**:
```javascript
// i18n을 위한 data-lang 속성 사용
// 언어 설정은 localStorage 키에 저장: 'bobpool-language'
switchLanguage(lang) // 'ko' 또는 'en'
```

**기능**:
- 부드러운 스크롤 네비게이션
- 스크롤 위치 기반 활성 섹션 강조
- 분석 이벤트 추적 (플레이스홀더)
- 버튼 키보드 접근성

## 문서 업데이트 워크플로우

### 법적 문서 변경 시

1. **마크다운 소스 업데이트**:
   - `privacy-policy-ko.md` 또는 `terms-of-service-ko.md` 편집
   - 시행일자 및 버전 번호 업데이트

2. **HTML 재생성**:
   - 마크다운을 HTML로 수동 변환 또는 빌드 스크립트 사용
   - HTML이 기존 페이지와 일관된 스타일을 유지하도록 확인
   - 내용 변경 시 한국어와 영어 버전 모두 업데이트

3. **버전 정보 업데이트**:
   ```html
   <!-- 각 HTML 파일에서 -->
   <p>시행일: YYYY-MM-DD</p>
   <p>최종 수정: YYYY-MM-DD</p>
   ```

4. **확인 체크리스트** (README.md:107-117):
   - [ ] 한국어 및 영어 문서 모두 업데이트
   - [ ] 시행일자 업데이트
   - [ ] 필요시 랜딩 페이지 요약 업데이트
   - [ ] 앱 상수 URL 일치 확인
   - [ ] 배포 후 링크 테스트
   - [ ] 모바일 접근성 테스트
   - [ ] 언어 전환 동작 확인

5. **배포**:
   ```bash
   git add .
   git commit -m "Update legal documents v1.x.x - [reason]"
   git push origin main
   ```

## 도메인 및 OAuth 설정

**중요 컨텍스트** (docs/OAuth 도메인 소유권 통과 플랜.md):

- **커스텀 도메인**: `legal.bobpool.app` (CNAME → GitHub Pages)
- **도메인 소유권**: Google Search Console을 통해 검증 (DNS TXT 레코드)
- **GCP OAuth**: 승인된 도메인은 `bobpool.app` (상위 도메인)
- **URL 패턴**: 항상 `https://legal.bobpool.app/[page].html` 사용

**Google Cloud Console의 OAuth URL**:
- 홈페이지: `https://legal.bobpool.app/`
- 개인정보처리방침: `https://legal.bobpool.app/privacy-policy.html`
- 이용약관: `https://legal.bobpool.app/terms-of-service.html`

**앱 통합**:
Flutter 앱 상수는 다음을 참조해야 함:
```dart
// lib/core/constants/legal_constants.dart
static const String legalWebsiteBaseUrl = 'https://legal.bobpool.app';
```

## 준수 요구사항

### 한국 법률 요구사항
- **개인정보보호법**: 개인정보처리방침은 데이터 수집, 사용, 보유, 제3자 제공에 대해 상세히 명시해야 함
- **전자상거래법**: 이용약관은 서비스 조건, 환불 정책, 분쟁 해결 절차를 명시해야 함
- **정보통신망법**: 쿠키 정책 및 동의 절차 명시

### 앱 스토어 요구사항
- **Apple App Store**: 개인정보처리방침 URL 필수, 앱 내에서 접근 가능해야 함
- **Google Play Store**: Play Console에 개인정보처리방침 URL 필수, 데이터 수집 공개

### 주요 연락처 정보
- 개인정보 문의: `tasddc@naver.com`
- 일반 문의: `tasddc@naver.com`
- 소재지: 대한민국 서울특별시

## 일반 유지보수 작업

### 새 언어 추가
1. 새 HTML 파일 생성: `privacy-policy-[lang].html`, `terms-of-service-[lang].html`
2. 헤더에 언어 버튼 추가:
   ```html
   <button class="lang-btn" onclick="switchLanguage('[lang]')">[Label]</button>
   ```
3. 모든 i18n 콘텐츠에 `data-lang="[lang]"` 속성 추가
4. 필요시 `switchLanguage()` 함수 업데이트
5. `manifest.json`에 새 언어 지원 업데이트

### 연락처 정보 업데이트
모든 HTML 파일에서 검색 및 교체:
- 이메일 주소
- 실제 주소 (해당하는 경우)
- 담당자/팀명

### 스타일 업데이트
모든 스타일은 `<style>` 태그에 인라인으로 작성됨. 주요 섹션:
- 전역 테마 변경을 위한 `:root` 변수
- 레이아웃 구조를 위한 `.header`, `.nav`, `.footer`
- 반응형 조정을 위한 미디어 쿼리 (끝부분)

## 배포 전 테스트

```bash
# 체크리스트
- [ ] 모든 내부 링크 작동
- [ ] 언어 전환이 localStorage에 선택사항 유지
- [ ] 모바일 반응형 (320px, 768px, 1200px 너비에서 테스트)
- [ ] legal.bobpool.app에서 HTTPS 인증서 유효
- [ ] 이메일 링크가 mailto: 프로토콜 사용
- [ ] 키보드로 콘텐츠 건너뛰기 링크 작동 (Tab 키)
- [ ] 고대비 모드 가독성
- [ ] 스크린 리더 호환성 (VoiceOver/NVDA로 테스트)
```

## 알려진 문제 및 해결방법

1. **GitHub Actions 경로 불일치**: 워크플로우가 `./legal-website`를 참조하지만 파일은 루트에 있음. 빌드 실패 시 `.github/workflows/deploy.yml` 경로를 `'.'`로 업데이트 필요.

2. **CNAME 파일**: 커스텀 도메인을 위해 저장소 루트에 반드시 존재해야 함. 현재 내용: `legal.bobpool.app`

3. **언어 표시 로직**: index.html의 710-714줄에 복잡한 표시 전환 로직. 인라인 스타일과 특정 요소 타입 체크 사용.

## 관련 리소스

- 메인 앱 저장소: BobPool Flutter 앱 (별도 저장소)
- 도메인 등록기관: [bobpool.app DNS 관리]
- Google Cloud Console: OAuth 동의 화면 설정
- Google Search Console: 도메인 소유권 검증
