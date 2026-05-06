# 김 비서 대시보드 (Kim Secretary Dashboard) - 프로젝트 정리

## 📋 프로젝트 개요

**프로젝트명**: Kim Secretary Dashboard (김 비서 - 데이터)  
**목적**: 마케팅 프로젝트 관리를 위한 프리미엄 glasmorphism 디자인 대시보드  
**배포**: Vercel (https://github.com/JYLEE6977/secretary_test)  
**기술 스택**: HTML5 + CSS3 + Vanilla JavaScript (외부 라이브러리 없음)

---

## 🎨 구현된 페이지

### 1. Dashboard (dashboard.html)
- **용도**: 메인 대시보드 페이지
- **레이아웃**: 4개 섹션 그리드
  - Todos (할 일 목록)
  - Schedule (일정)
  - Projects (프로젝트 목록)
  - Sales (매출)
- **특징**: 
  - Sticky 헤더와 네비게이션
  - 프리미염 glasmorphism 디자인
  - Dark/Light 모드 지원
  - LocalStorage에 테마 설정 저장

### 2. Chart (chart.html)
- **용도**: 매출 분석 및 시각화
- **그래프**:
  - 라인 차트: 월별 매출 (Sales Analysis)
  - 바 차트: 제품별 매출 (By Product)
- **기술**: Canvas API로 직접 그래프 렌더링 (Chart.js 등 라이브러리 미사용)
- **특징**: Sticky 네비게이션, 반응형 캔버스

### 3. Diagram (diagram.html + diagram.svg)
- **용도**: 마케팅 프로젝트 5단계 워크플로우 시각화
- **프로세스**: 
  1. 기획 (Planning) - Purple
  2. 제작 (Production) - Blue
  3. 검토 (Review) - Amber
  4. 배포 (Deploy) - Green
- **기술**: SVG 벡터 그래픽
- **특징**: 인터랙티브 호버 효과, Shadow 효과

### 4. Report (report.html)
- **용도**: SubTrackr 웹사이트 분석 보고서
- **내용**: 사이트 구조, 디자인, 기능 분석
- **레이아웃**: 카드 기반 섹션

---

## 🎯 주요 기능

### 네비게이션
```
대시보드 → 회의록 → 매출 현황 → 업무 프로세스 → 사이트 분석
```
- 모든 페이지에서 접근 가능
- 현재 페이지 강조 표시 (Active state)
- Sticky positioning으로 항상 상단 고정

### Dark/Light Mode
- 토글 버튼으로 테마 전환
- LocalStorage에 사용자 선택 저장
- 다크 모드: 어두운 배경 + 밝은 텍스트
- 라이트 모드: 밝은 배경 + 어두운 텍스트

### Glassmorphism UI
- 반투명 배경: `rgba(255,255,255,0.05)`
- Blur 효과: `backdrop-filter: blur(24px)`
- Shadow: `0 8px 32px rgba(0,0,0,0.45)`
- 부드러운 전환: `0.35s cubic-bezier(.4,0,.2,1)`

---

## 🛠️ 기술 세부사항

### CSS 설계
- **CSS Variables** 활용으로 테마 관리
- Dark/Light 모드별 색상 정의
- 모든 애니메이션에 일관된 transition 사용

```css
:root {
  --transition: 0.35s cubic-bezier(.4,0,.2,1);
}

[data-theme="dark"] {
  --bg-base: #0f0f23;
  --text-primary: #e8e8f0;
  --glass-bg: rgba(255,255,255,0.05);
  /* ... */
}
```

### 색상 팔레트
| 용도 | 색상 | 코드 |
|------|------|------|
| 기획 | Purple | #a78bfa |
| 제작 | Blue | #60a5fa |
| 검토 | Amber | #f59e0b |
| 배포 | Green | #4ade80 |

### 폰트
- 주 폰트: 'Segoe UI', 'Apple SD Gothic Neo', 'Noto Sans KR', sans-serif
- 일관된 폰트로 크로스 플랫폼 지원

### JavaScript 기능
```javascript
// 테마 전환
applyTheme(theme) // 'dark' | 'light'

// 네비게이션 활성화
activateCurrentNav() // 현재 페이지 감지 및 강조
```

---

## 🔧 해결된 이슈

### Issue 1: 네비게이션 색상 불일치
**문제**: 메뉴바 뒤 배경색이 어울리지 않음  
**원인**: 불투명한 배경 색상 사용  
**해결**: 
- 배경을 반투명(`rgba(15,15,35,0.4)`)으로 변경
- `backdrop-filter: blur(12px)` 추가
- Glass effect로 자연스럽게 통합

### Issue 2: GitHub 토큰 보안
**문제**: 로컬 환경에서 GitHub 토큰 관리 필요  
**해결**:
- `.env` 파일 생성 (로컬에만 존재)
- `.env.example` 템플릿 제공
- `.gitignore`에 `.env` 추가로 커밋 방지

### Issue 3: Vercel 배포 404 에러
**문제**: 루트 경로(`/`) 접근 시 404 에러  
**원인**: index.html 부재  
**해결**: 
```html
<!-- index.html 생성 -->
<!DOCTYPE html>
<html>
<head>
  <title>김 비서 대시보드</title>
  <script>
    window.location.href = 'dashboard.html';
  </script>
</head>
</html>
```
- index.html 생성으로 루트 경로 처리
- dashboard.html로 자동 리다이렉트

---

## 📁 파일 구조

```
워크숍-실습/
├── .env                    # GitHub 토큰 (커밋 안 됨)
├── .env.example            # 환경 변수 템플릿
├── .gitignore              # git 무시 파일
├── .git/                   # GitHub 저장소
│
├── index.html              # 루트 경로 (dashboard.html로 리다이렉트)
├── dashboard.html          # 메인 대시보드
├── chart.html              # 매출 분석 차트
├── diagram.html            # 프로세스 다이어그램 (HTML 래퍼)
├── diagram.svg             # SVG 다이어그램 (별도 파일)
└── report.html             # 웹사이트 분석 보고서
```

---

## 🚀 배포 및 운영

### GitHub Repository
- **URL**: https://github.com/JYLEE6977/secretary_test
- **인증**: Fine-grained Personal Access Token (읽기/쓰기 권한)
- **저장소 타입**: Public

### Vercel 배포
- **플랫폼**: Vercel (정적 사이트 호스팅)
- **배포 방식**: GitHub 자동 연동
  - GitHub에 push → Vercel 자동 배포
  - 배포 시간: 약 1-2분
- **배포 파일**: 모든 HTML, CSS, SVG 파일

### 환경 설정
1. `.env` 파일에 GitHub 토큰 입력
2. `.env`는 로컬에만 존재 (git에 커밋되지 않음)
3. Vercel 환경 변수는 별도 설정 필요시 대시보드에서 구성

---

## 📝 개발 가이드

### 새로운 페이지 추가 시
1. HTML 파일 생성 (예: `new-page.html`)
2. 기본 구조 (header, nav, content) 포함
3. 네비게이션에 링크 추가:
   ```html
   <a href="new-page.html" class="nav-btn nav-item" data-page="new-page">
     <span class="nav-icon">🔧</span>
     <span>새 페이지</span>
   </a>
   ```
4. CSS 및 JavaScript 통합

### 스타일 수정 시
- CSS 변수 활용 (일관성 유지)
- Dark/Light 모드 모두 테스트
- Glassmorphism 특성 유지

### 배포 전 체크리스트
- [ ] 모든 링크 정상 작동 확인
- [ ] Dark/Light 모드 테스트
- [ ] 반응형 디자인 확인 (모바일/태블릿/데스크톱)
- [ ] `.env` 파일이 `.gitignore`에 포함되어 있는지 확인
- [ ] `git push` 후 Vercel 배포 확인

---

## 💡 다음 아이디어 추진 시

새로운 기능이나 수정사항이 필요할 때는 다음 정보를 참고하세요:
- 전체 프로젝트 구조 위 파일 구조 참고
- 색상 팔레트와 CSS 변수 활용
- Glassmorphism 디자인 일관성 유지
- Vanilla JavaScript로 구현 (외부 라이브러리 미사용 정책)
- 배포는 GitHub push → Vercel 자동 배포 방식

---

**최종 업데이트**: 2026-05-06  
**상태**: 배포 완료, 정상 운영 중

