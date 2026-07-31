# 바다윈디 공개 데이터

[바다윈디](https://play.google.com/store/apps/details?id=com.badamobile.bada_mobile)
앱이 실행 중에 내려받는 **공개 파일**만 두는 저장소입니다. 앱 소스 코드는
비공개 저장소에 있습니다.

| 파일 | 용도 |
|---|---|
| `wind_field.json.gz` (릴리스 `wind-data`) | 지도 바람장 격자. 자동 갱신(하루 8회) |
| `app_gate.json` | 강제 업데이트 안내 설정 |
| `privacy-policy.html` | 개인정보처리방침 ([보기](https://bisan74-lab.github.io/badawindy-data/privacy-policy.html)) |

## 데이터 출처

- 바람·해양: [Open-Meteo](https://open-meteo.com/) (ECMWF IFS / WAM, GFS Wave)
- 조석·낚시지수: 국립해양조사원·해양수산부 공공데이터
- 날씨: 기상청

## 주의

`wind_field.json.gz`는 비공개 저장소의 GitHub Actions 크론이 자동으로 덮어씁니다.
직접 수정하지 마세요.

`app_gate.json`의 `forceUpgrade`를 `true`로 바꾸면 **설치된 모든 기기에서 앱 실행이
막히고** 업데이트 안내만 표시됩니다. 앱 재배포 없이 즉시 적용되므로 신중히 다루세요.
