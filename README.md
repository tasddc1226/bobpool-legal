# BobPool Legal Documents Website

이 디렉토리에는 BobPool 앱의 법적 문서들과 관련 웹사이트가 포함되어 있습니다.

## 파일 구조

```
legal-website/
├── index.html                    # 메인 랜딩 페이지 (다국어 지원)
├── privacy-policy.html           # 한국어 개인정보처리방침
├── privacy-policy-en.html        # 영어 개인정보처리방침
├── terms-of-service.html         # 한국어 서비스 이용약관
├── terms-of-service-en.html      # 영어 서비스 이용약관
├── privacy-policy-ko.md          # 한국어 개인정보처리방침 (원본)
├── terms-of-service-ko.md        # 한국어 서비스 이용약관 (원본)
├── CNAME                         # 커스텀 도메인 설정
└── .github/workflows/deploy.yml  # GitHub Pages 자동 배포
```

## 기술 특징

### 접근성 (WCAG 2.1 AA 준수)
- 스크린 리더 지원
- 키보드 네비게이션
- 고대비 색상 사용
- 의미론적 HTML 구조
- Skip to content 링크

### 반응형 디자인
- Mobile-first 접근법
- 유연한 그리드 레이아웃
- 터치 친화적 인터페이스
- 다양한 화면 크기 지원

### 다국어 지원
- 한국어 (기본)
- 영어
- JavaScript로 언어 전환
- localStorage에 언어 설정 저장

### 성능 최적화
- 인라인 CSS로 HTTP 요청 최소화
- 압축된 이미지
- 캐시 최적화된 헤더
- 빠른 로딩 시간

## 배포

이 웹사이트는 GitHub Pages를 통해 자동으로 배포됩니다:

1. **도메인**: `legal.bobpool.app`
2. **HTTPS**: 자동으로 제공됨
3. **자동 배포**: main 브랜치의 legal-website/ 폴더 변경시 자동 트리거

### 수동 배포

```bash
# 1. 변경사항 커밋
git add legal-website/
git commit -m "Update legal documents"

# 2. 메인 브랜치에 푸시
git push origin main

# 3. GitHub Actions에서 자동으로 배포됨
```

## 법적 요구사항 준수

### 한국 개인정보보호법
- 개인정보 처리목적 명시
- 처리 및 보유기간 명시
- 제3자 제공 현황 공개
- 개인정보보호책임자 연락처

### 전자상거래법
- 서비스 제공 조건 명시
- 청약철회 및 환급 정책
- 분쟁 해결 절차
- 준거법 및 재판관할 명시

### 정보통신망법
- 개인정보 수집·이용 고지
- 동의 절차 구현
- 쿠키 정책 명시

## 연락처

- **개인정보 관련**: tasddc@naver.com
- **일반 문의**: tasddc@naver.com
- **법무 관련**: tasddc@naver.com

## 버전 관리

- **문서 버전**: 1.0.0
- **시행일**: 2025-01-01
- **최종 수정**: 2025-01-01

### 변경 이력

| 날짜 | 버전 | 변경사항 |
|------|------|----------|
| 2025-01-01 | 1.0.0 | 초기 버전 생성 |

## 개발자 가이드

### 법적 문서 업데이트 시 체크리스트

1. [ ] 개인정보처리방침 업데이트 (한국어/영어)
2. [ ] 이용약관 업데이트 (한국어/영어)
3. [ ] 시행일자 및 수정일자 업데이트
4. [ ] 메인 페이지 요약 내용 업데이트
5. [ ] 앱 내 상수 파일 URL 확인
6. [ ] 배포 후 링크 동작 확인
7. [ ] 모바일 접근성 테스트
8. [ ] 다국어 표시 확인

### 코드 스타일

- Semantic HTML5 사용
- CSS Custom Properties 활용
- BEM 네이밍 컨벤션 (선택적)
- Progressive Enhancement 원칙 적용

## 라이선스

이 프로젝트는 BobPool의 사유 재산입니다. 무단 복제 및 배포를 금지합니다.