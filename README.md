# 바로기획 홈페이지

정적 사이트 — GitHub Pages 로 배포: https://brizymedia.github.io/baro-event/

제작: 큰길브리지 (주식회사 브리지미디어)

## 업무 도구 (2026-10-01, 큰길이벤트기획 기능을 옮김)

| 기능 | 주소 | 서버 |
|---|---|---|
| 자동 견적서(손님용) | `quote.html` | 문의 서버(공용) |
| 견적서 발행 · 저장함(관리자) | `quote.html?admin=1` | 저장함 폰·PC 같이 보기는 계약 서버 |
| 전자계약서 | `contract.html?admin=1` | 계약 서버(`apps-script/contract`) — 없으면 서명 통보만 메일로 |
| 거래명세서 | `statement.html?admin=1` | 없음 |
| 사진 올리기 + 블로그 · 인스타 글 만들기 | `upload.html` | 갤러리 서버(`apps-script/gallery`) → `photos` 가지 → 현장사진 페이지 |
| 행사 이야기 | `stories/` | 없음 — `python tools/make_pages.py` |
| 지역 페이지 | `areas/` | 없음 — 같은 명령 |
| 문의 알림 | `contact.html` 폼 · 견적서 | 문의 서버 → 대표 메일 + 큰길브리지 |
| 행사 일정 · 체크리스트 | `schedule.html` | 계약 서버(일정 기능 — 2026-10-03 새 코드, 재배포 + 스크립트 속성 `CREW_PW` 필요) |
| 대표 전용 업무 문서함 | `office.html` | 없음 — 도구 모음 · 서버 연결 상태 · 암호 안내(noindex) |
| 유입 현황 · AI 검색 | `stats.js` · `llms.txt` · `sitemap.xml` · `robots.txt` | 큰길브리지 유입 서버 |

- 서류 3종 · `upload.html` · `schedule.html` · `quote-catalog.js` · 서버 코드 · `office.html` 은 큰길이벤트 원본에서 `python tools/port_docs.py` 로 옮긴다(원본이 바뀌면 다시 돌리면 됨). 바로기획 쪽 손수정은 그 스크립트 안에 규칙으로 넣을 것.
- 직인: `assets/img/stamp-baro.png` (투명 PNG) 가 생기면 계약서 · 명세서에 찍힌다. 없으면 「(인)」 자리만.
- 계약 서버 주소가 정해지면 `tools/port_docs.py` 의 `BARO_CONTRACT` 에 넣고 다시 돌린다.

## 행사 준비 블로그 (2026-10-28, HD기획 _blog 루틴을 옮김)

- 원본 `_blog/posts/<날짜>-<slug>.json` → `node scripts/build-blog.mjs` → `/blog/`(목록 · 지역 모음 · 글) + `rss.xml` + sitemap.xml · llms.txt 의 블로그 부분. 결과 HTML 은 손으로 고치지 말 것.
- 규칙은 `_blog/GUIDE.md`. 지역 자료 `_blog/regions.json`(make_pages.py AREAS 9곳 · 현장기록), 주제 `_blog/keywords.json`, 사진 `_blog/photos.json`(얼굴 큰 사진 7장 제외), 공식 출처 `_blog/sources.json`.
- 쓰기 전 `node scripts/blog-plan.mjs`, 쓴 뒤 `node scripts/blog-check.mjs --new <파일>` 통과해야 올린다(가격 · 후기 · 인원 수 · 설립 연도 · 경력 연수 · 다른 회사 이름 · 지어낸 지역 이야기를 막는다).
- `python tools/make_pages.py` 는 sitemap.xml 을 통째로 다시 쓰므로 돌린 뒤 `node scripts/build-blog.mjs` 를 다시 돌린다.
- 블로그 글의 주소(canonical)는 www.바로기획.com 기준이다. 나머지 페이지 canonical · sitemap · robots.txt 는 아직 brizymedia.github.io/baro-event 주소다.
