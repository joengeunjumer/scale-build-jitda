# SCALE BUILD (짓다 · JITDA)

노후 건물 **파사드 리노베이션 사업을 위한 마케팅 리드 엔진 + 공공데이터 처리 파이프라인**입니다. Scale Virtual 인턴십에서 바이브 코딩(Claude Code)으로 구축했습니다.

> An AI-assisted marketing lead engine and open-data pipeline for a facade-renovation business: a static-frontend lead funnel with AI render preview, plus Python scripts that turn Korean government building-registry data into geocoded, priority-scored prospect maps.

> 🔒 **소스 코드는 private 저장소로 관리합니다** (개인정보·비즈니스 데이터는 저장소에서 완전히 제외). 열람이 필요하시면 연락 주세요 — joengeunjumer@gmail.com

## 구성 요소

### ① 마케팅 리드 퍼널 (웹 프론트엔드)
건물주가 주소를 입력하면 **AI 파사드 리노베이션 렌더링 미리보기**를 보여주고 상담 신청으로 연결하는 퍼널. 정적 HTML/JS + Supabase로 서버 없이 운영하고 Vercel로 배포합니다.

- 키 분리 설계: `config.js`(공개) / `config.local.js`(배포 시 환경변수로 주입, 저장소 미포함)
- 데모 폴백: API 키 없이도 데모 렌더로 퍼널 전체 체험 가능

### ② 건축물대장 데이터 파이프라인 (Python)
공공데이터포털의 건축물대장 표제부에서 **강남권 노후 근생 꼬마빌딩 후보를 추출·점수화**하는 파이프라인:

```
표제부 CSV ─→ 필터(RC·근생·규모) ─→ 적합도 점수화(연식 스윗스팟 곡선) ─→ 지오코딩 ─→ 체크지도(Leaflet) + 우편 라벨
```

- **적합도 알고리즘**: 오래될수록 좋은 게 아니라 "구조 손 안 대고 외피 시공이 가능한 적정 노후 구간(약 18~28년)"이 최고점인 스윗스팟 곡선 설계
- **가드레일 문서화**: 자동 크롤링 금지, 데이터 취득 단계는 사람이 직접 — AI 협업 시 넘지 말아야 할 선을 `CLAUDE.md`에 명시

### ③ 팀 업무 캘린더 (Node.js)
로컬 네트워크에서 공유하는 단일 파일 팀 캘린더 (server.js + HTML).

## 기술 스택

HTML/CSS/JavaScript · Python (pandas·openpyxl) · Node.js · Supabase · Kakao/Naver Maps API · Vercel

## 바이브 코딩 프로세스

파이프라인의 각 단계(파싱→필터→지오코딩→지도 생성→라벨)를 Claude Code와 스크립트 단위로 개발했습니다. 특히 **`CLAUDE.md` 인수인계 문서** — AI에게 프로젝트 컨텍스트와 가드레일을 넘기는 문서 — 를 작성해 사람↔AI 협업 워크플로우 자체를 설계했습니다.
