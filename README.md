# 바다윈디 공개 데이터

[바다윈디](https://play.google.com/store/apps/details?id=com.badamobile.bada_mobile)
앱이 실행 중에 내려받는 **공개 파일**과, 그 파일을 만드는 **데이터 수집
크론**을 두는 저장소입니다. 앱 소스 코드는
[BadaMobile](https://github.com/bisan74-lab/BadaMobile)에 있습니다(현재 공개).

| 파일 | 용도 |
|---|---|
| `wind_field.json.gz` (릴리스 `wind-data`) | 지도 바람장 격자. 자동 갱신(하루 8회) |
| `point_forecast.json.gz` (릴리스 `point-forecast`) | 홈·낚시정보 카드 예보. 자동 갱신(3시간 간격) |
| `fishing_index.json.gz` (릴리스 `fishing-data`) | 낚시지수. 자동 갱신(하루 4회) |
| `app_gate.json` | 강제 업데이트 안내 설정 |
| `privacy-policy.html` | 개인정보처리방침 ([보기](https://bisan74-lab.github.io/badawindy-data/privacy-policy.html)) |

## 데이터 수집 크론 (`.github/workflows/`)

세 릴리스 파일은 이 저장소 자신의 GitHub Actions가 만든다(2026-08-08부터 —
그전엔 BadaMobile의 크론이 만들어 여기로 올렸다). **수집 스크립트는 여기
없다** — 매 실행마다 [BadaMobile](https://github.com/bisan74-lab/BadaMobile)을
읽기 전용으로 체크아웃해 `tool/fetch_*.py`를 그대로 돌린다. 스크립트를 여기
복사해 두면 BadaMobile 쪽만 고치고 잊어버리는 사고가 나므로, 코드는 항상
BadaMobile 한 곳에만 있다.

**BadaMobile 쪽 크론과 대체 관계다** — BadaMobile이 지금은 공개 저장소라
저장소를 나눠 둘 필요가 없어졌지만(예전엔 비공개 저장소의 GitHub Pages가
유료 플랜 전용이라 정책 문서·데이터만 여기로 뺐다), 코드와 데이터를 분리해
두는 게 정리에 낫다고 판단해 크론만 여기로 옮겼다. 결과를 자기 자신에게
올리므로 저장소 간 PAT 없이 기본 `GITHUB_TOKEN`으로 충분하다.

`fishing-data.yml`은 `DATA_GO_KR_API_KEY` Secret이 필요하다 — 이 저장소
Settings → Secrets and variables → Actions에 BadaMobile에 등록된 것과 같은
값으로 새로 등록해야 한다(Secret 값은 저장소 간에 자동으로 넘어오지 않는다).

## 데이터 출처

- 바람·해양: [Open-Meteo](https://open-meteo.com/) (ECMWF IFS / WAM, GFS Wave)
- 조석·낚시지수: 국립해양조사원·해양수산부 공공데이터
- 날씨: 기상청

## 주의

`wind_field.json.gz`·`point_forecast.json.gz`·`fishing_index.json.gz`는
이 저장소의 GitHub Actions 크론이 자동으로 덮어씁니다. 직접 수정하지 마세요.

`app_gate.json`의 `forceUpgrade`를 `true`로 바꾸면 **설치된 모든 기기에서 앱 실행이
막히고** 업데이트 안내만 표시됩니다. 앱 재배포 없이 즉시 적용되므로 신중히 다루세요.
