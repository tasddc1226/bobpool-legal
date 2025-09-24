# BobPool 법적 문서 웹사이트 배포 가이드

이 가이드는 BobPool 앱의 스토어 배포를 위한 필수 법적 문서 웹사이트 설정 및 배포 방법을 설명합니다.

## 🚀 빠른 배포 가이드 (추천)

### Option 1: GitHub Pages (무료, 추천)

1. **GitHub 저장소 설정**
   ```bash
   # 현재 저장소를 GitHub에 푸시
   git add .
   git commit -m "Add legal documents website"
   git push origin main
   ```

2. **GitHub Pages 활성화**
   - GitHub 저장소 → Settings → Pages
   - Source: "Deploy from a branch" 선택
   - Branch: `main` 선택, Folder: `/ (root)` 선택
   - 또는 GitHub Actions을 통한 자동 배포 사용

3. **커스텀 도메인 설정**
   - Pages 설정에서 Custom domain에 `legal.bobpool.app` 입력
   - DNS 설정에서 CNAME 레코드 추가:
     ```
     legal.bobpool.app → your-username.github.io
     ```

### Option 2: Vercel (추천, 더 빠른 설정)

1. **Vercel 계정 생성 및 연결**
   ```bash
   npm i -g vercel
   vercel login
   cd legal-website
   vercel
   ```

2. **도메인 설정**
   - Vercel 대시보드에서 프로젝트 선택
   - Domains 탭에서 `legal.bobpool.app` 추가
   - DNS 설정에서 CNAME 레코드 추가

### Option 3: Netlify

1. **Netlify Deploy**
   - Netlify 웹사이트에서 "Add new site" → "Deploy manually"
   - `legal-website` 폴더를 드래그 앤 드롭

2. **도메인 설정**
   - Site settings → Domain management
   - Add custom domain: `legal.bobpool.app`

## 🔧 상세 설정 가이드

### 1. 도메인 구매 및 DNS 설정

#### 도메인명 추천
- `legal.bobpool.app` (서브도메인, 추천)
- `bobpool-legal.com`
- `bobpool.legal`

#### DNS 설정 예시 (GitHub Pages)
```
Type: CNAME
Name: legal
Value: your-username.github.io
TTL: 3600
```

#### DNS 설정 예시 (Vercel)
```
Type: CNAME
Name: legal
Value: cname.vercel-dns.com
TTL: 3600
```

### 2. HTTPS 인증서 설정

대부분의 호스팅 서비스(GitHub Pages, Vercel, Netlify)는 자동으로 Let's Encrypt SSL 인증서를 제공합니다.

**확인 방법:**
- 배포 후 `https://legal.bobpool.app`로 접속
- 브라우저에서 자물쇠 아이콘 확인
- SSL Labs Test로 보안 등급 확인

### 3. 앱 스토어 정책 준수 확인

#### Apple App Store
- [x] 개인정보처리방침 URL 필수
- [x] 앱 내에서 직접 접근 가능
- [x] 사용자가 읽기 쉬운 형태
- [x] 한국어 지원 (한국 출시시)

#### Google Play Store
- [x] 개인정보처리방침 URL 필수
- [x] Google Play Console에 URL 등록
- [x] 개발자 정책 준수
- [x] 데이터 수집 내역 정확히 기재

### 4. Flutter 앱 연동 확인

```dart
// lib/core/constants/legal_constants.dart 확인
static const String legalWebsiteBaseUrl = 'https://legal.bobpool.app';
```

**테스트 항목:**
- [ ] 회원가입시 법적 문서 동의 체크박스 표시
- [ ] 개인정보처리방침 링크 동작
- [ ] 이용약관 링크 동작
- [ ] 설정 화면에서 법적 문서 접근 가능
- [ ] 외부 브라우저에서 정상 열림

## 🔍 배포 후 검증 체크리스트

### 기술적 검증
- [ ] HTTPS 인증서 정상 동작
- [ ] 모든 페이지 로딩 확인
- [ ] 모바일 반응형 디자인 확인
- [ ] 다국어 전환 기능 확인
- [ ] 외부 링크 (이메일 등) 동작 확인
- [ ] 접근성 도구로 WCAG 준수 확인

### 법적 요구사항 검증
- [ ] 개인정보처리방침 완전성 확인
- [ ] 이용약관 완전성 확인
- [ ] 연락처 정보 정확성 확인
- [ ] 시행일자 정확성 확인
- [ ] Supabase 데이터 처리 내역 정확성

### 앱 스토어 정책 검증
- [ ] Apple App Store 정책 준수 확인
- [ ] Google Play Store 정책 준수 확인
- [ ] 데이터 수집 내역과 앱 기능 일치성
- [ ] 사용자 동의 절차 적절성

## 📱 앱 스토어 등록

### Apple App Store
1. App Store Connect → 앱 정보 → Privacy Policy URL
2. URL: `https://legal.bobpool.app/privacy-policy.html`
3. 한국 출시: `https://legal.bobpool.app/privacy-policy.html`

### Google Play Store
1. Play Console → 정책 → 앱 콘텐츠
2. 개인정보 보호정책: `https://legal.bobpool.app/privacy-policy-en.html`
3. 데이터 보안 섹션에서 데이터 수집 내역 입력

## 🔄 업데이트 및 유지보수

### 정기적 검토 항목 (분기별)
- [ ] 법령 변경사항 반영
- [ ] 앱 기능 변경에 따른 정책 업데이트
- [ ] 연락처 정보 확인
- [ ] 링크 동작 상태 확인
- [ ] SSL 인증서 갱신 상태 확인

### 업데이트 프로세스
1. 문서 수정 (legal-website/*.html)
2. 버전 정보 업데이트 (날짜, 버전)
3. Git 커밋 및 푸시
4. 자동 배포 대기 (2-3분)
5. 배포 확인 및 테스트

## ⚠️ 중요 사항

### 데이터 처리 정확성
- Supabase를 통한 데이터 처리 내역이 정확히 기재되어 있는지 확인
- 수집하는 개인정보 항목과 앱의 실제 수집 항목이 일치하는지 확인
- 제3자 제공 현황 (Supabase, Google Analytics 등) 정확성 확인

### 연락처 관리
- tasddc@naver.com: 개인정보 관련 문의
- tasddc@naver.com: 일반 서비스 문의
- tasddc@naver.com: 기타 법무 관련 문의

### 백업 및 복구
- 법적 문서는 항상 원본 파일(Markdown) 보관
- Git 이력을 통한 변경사항 추적
- 중요한 변경시 수동 백업 권장

## 🆘 트러블슈팅

### 일반적인 문제

**1. 도메인이 연결되지 않음**
- DNS 전파 시간 대기 (최대 48시간)
- DNS 설정 재확인
- `dig legal.bobpool.app` 명령어로 확인

**2. HTTPS 인증서 오류**
- DNS 설정 확인 후 24시간 대기
- 호스팅 서비스의 SSL 설정 확인
- 브라우저 캐시 클리어

**3. 앱에서 링크가 열리지 않음**
- URL 상수 확인
- url_launcher 패키지 설정 확인
- 디바이스의 기본 브라우저 설정 확인

### 연락처
- **기술적 문제**: GitHub Issues 또는 개발팀
- **법적 문의**: tasddc@naver.com
- **긴급 상황**: 즉시 개발팀 연락

---

**이 가이드를 따라하면 스토어 배포에 필요한 모든 법적 문서 요구사항을 충족할 수 있습니다.**