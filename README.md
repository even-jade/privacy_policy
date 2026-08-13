# privacy_policy

Yoni.Gyun 이 만든 앱들의 **개인정보 처리방침을 게시하는 저장소**다.
GitHub Pages 로 서비스되며, 여기 있는 URL 이 각 앱의 스토어 등록정보에 들어간다.

**게시 주소**: https://even-jade.github.io/privacy_policy/

> ⚠️ **이 주소는 GitHub username 에 묶여 있다.**
>
> username 을 바꾸면 저장소 URL(`github.com/<user>/repo`)은 GitHub 이 리다이렉트해 주지만
> **Pages 주소(`<user>.github.io`)는 리다이렉트되지 않고 그대로 404 가 된다.**
> 2026-08 에 `minkyunkim-kor` → `even-jade` 로 바꿨을 때 실제로 방침 URL 이 죽었다.
>
> 처리방침 URL 접근 불가는 **Play 심사 반려 사유**다. username 을 바꾸면 반드시:
> 1. 이 README 의 주소들
> 2. 각 앱 저장소의 문서(TripTable 은 `README.md`, `STORE_LISTING.md`)
> 3. **Play Console 의 개인정보 처리방침 입력값**
>
> 세 곳을 함께 고친다. 3번을 빠뜨리면 스토어에 죽은 링크가 걸린 채로 남는다.
>
> 주소가 username 에 묶이는 게 부담되면 커스텀 도메인을 붙이는 방법도 있다.

---

## 게시된 방침

| 앱 | 한국어 (정본) | English |
|----|--------------|---------|
| TripTable | [/triptable/](https://even-jade.github.io/privacy_policy/triptable/) | [/triptable/en/](https://even-jade.github.io/privacy_policy/triptable/en/) |

---

## 구조

```
privacy_policy/
├── index.html              # 허브 — 앱 목록
├── assets/
│   └── policy.css          # 모든 방침이 공유하는 스타일
├── triptable/
│   ├── index.html          # 한국어 (정본)
│   └── en/index.html       # 영문
└── .nojekyll               # Jekyll 빌드 건너뛰기
```

앱마다 최상위에 디렉터리 하나를 둔다. 디렉터리 이름이 곧 URL 이므로
**소문자·하이픈**으로 짓고, 한 번 스토어에 등록한 뒤에는 바꾸지 않는다.

`index.html` 을 쓰는 이유는 URL 에서 `.html` 을 없애기 위해서다
(`/triptable/` 가 `/triptable/privacy-policy.html` 보다 스토어 등록정보에 넣기 좋다).

---

## 새 앱 추가하기

1. `<앱이름>/index.html` 을 만든다. 기존 `triptable/index.html` 을 복사해 쓰는 게 빠르다.
2. 스타일은 인라인으로 넣지 말고 공통 시트를 링크한다.
   - 최상위 앱 디렉터리에서: `<link rel="stylesheet" href="../assets/policy.css">`
   - 한 단계 더 깊은 곳(`en/`)에서: `../../assets/policy.css`
3. 영문판이 필요하면 `<앱이름>/en/index.html` 에 둔다.
4. 최상위 `index.html` 의 앱 목록에 한 줄 추가한다.
5. `main` 에 push 하면 몇 분 안에 반영된다.

---

## 방침을 쓸 때 지킬 것

문서가 앱의 **실제 동작과 다르면 Play 데이터 안전 양식과 어긋나** 심사에서 문제가 된다.
빈칸을 채우는 생성기 결과를 그대로 쓰지 말고 아래를 직접 확인한다.

- **매니페스트 병합 결과의 실제 권한 목록**을 기준으로 쓴다. SDK 가 몰래 넣는 권한이 있다.
  Firebase Analytics 는 `com.google.android.gms.permission.AD_ID` 를 추가하므로
  "익명 데이터만 수집" 같은 문장은 거짓이 된다.
  ```bash
  ./gradlew :app:assembleRelease
  # app/build/intermediates/merged_manifest/release/**/AndroidManifest.xml 확인
  ```
- **수집하지 않는 것도 적는다.** 특히 사용자가 입력한 데이터가 기기 밖으로 나가지 않는다면
  그 사실이 문서에서 가장 중요한 문장이다. Play 데이터 안전 양식의 "수집 안 함" 신고와
  방침을 일치시키는 근거가 된다.
- **개발자 이름은 Play Console 의 공개 개발자 이름과 정확히 일치**시킨다.
- 보유 기간은 Firebase 콘솔의 실제 설정값과 대조한다 (기본값을 그대로 적지 않는다).
- 국내 출시 앱은 **한국어를 정본**으로 한다. PIPA 는 개인정보 보호책임자 명시와
  국외이전 고지 항목을 요구한다.

---

## 방침을 고쳐야 하는 시점

코드 변경뿐 아니라 **콘솔 설정 변경도 방침을 거짓으로 만든다.** 방침은 코드와 설정
양쪽에 걸쳐 있다.

### 코드 변경

- 광고 SDK 도입 (수집·제3자 공유 항목이 늘어난다)
- 인앱결제 도입
- 분석·크래시 도구 추가·교체
- 서버 도입 등 데이터가 기기 밖으로 나가게 되는 모든 변경

### 콘솔 설정 변경

방침이 근거로 삼는 값 중 **되돌릴 수 있는 설정**이 있다. 이걸 바꾸면 방침과
Play 데이터 안전 양식을 **둘 다** 고쳐야 한다.

| 설정 | 현재 | 방침에서 근거로 쓰는 문장 |
|------|------|--------------------------|
| GA4 · 세부 위치 및 기기 데이터 수집 | **꺼짐** | "도시·기기 모델·화면 해상도를 수집하지 않는다", 데이터 안전 양식의 "위치 = 수집 안 함" |
| GA4 · 데이터 보관 기간 | **14개월** | 수집 항목 표의 보유 기간 |

특히 위치 항목은, 이 설정을 켜는 순간 GA4 가 도시 단위를 수집하기 시작해
데이터 안전 양식의 "대략적인 위치 = 수집 안 함" 신고가 **사실과 달라진다.**

---

변경 시 문서의 **시행일을 갱신**하고, 이용자에게 불리한 변경은 시행 7일 전에 게시한다.
