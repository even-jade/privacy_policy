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
> 2. 각 앱 저장소의 문서(여행첩은 `README.md`, `STORE_LISTING.md`)
> 3. **Play Console 의 개인정보 처리방침 URL 과 데이터 삭제 요청 URL 입력값**
>
> 세 곳을 함께 고친다. 3번을 빠뜨리면 스토어에 죽은 링크가 걸린 채로 남는다.
>
> 주소가 username 에 묶이는 게 부담되면 커스텀 도메인을 붙이는 방법도 있다.

---

## 게시된 방침

| 앱 | 문서 | 한국어 (정본) | English |
|----|------|--------------|---------|
| 여행첩 (구 TripTable) | 처리방침 | [/triptable/](https://even-jade.github.io/privacy_policy/triptable/) | [/triptable/en/](https://even-jade.github.io/privacy_policy/triptable/en/) |
| 여행첩 (구 TripTable) | 계정·데이터 삭제 요청 | [/triptable/delete/](https://even-jade.github.io/privacy_policy/triptable/delete/) | [/triptable/en/delete/](https://even-jade.github.io/privacy_policy/triptable/en/delete/) |

---

## 구조

```
privacy_policy/
├── index.html              # 허브 — 앱 목록
├── assets/
│   └── policy.css          # 모든 방침이 공유하는 스타일
├── triptable/
│   ├── index.html          # 처리방침 한국어 (정본)
│   ├── delete/index.html   # 계정·데이터 삭제 요청 한국어 (정본)
│   └── en/
│       ├── index.html          # 처리방침 영문
│       └── delete/index.html   # 계정·데이터 삭제 요청 영문
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
   - 한 단계 더 깊은 곳(`en/`, `delete/`)에서: `../../assets/policy.css`
   - 두 단계 더 깊은 곳(`en/delete/`)에서: `../../../assets/policy.css`
3. 영문판이 필요하면 `<앱이름>/en/index.html` 에 둔다.
4. 최상위 `index.html` 의 앱 목록에 한 줄 추가한다.
5. `main` 에 push 하면 몇 분 안에 반영된다.

---

## 데이터 삭제 요청 페이지

계정을 만드는 앱은 Play Console 의 데이터 안전 양식에 **앱을 설치하지 않고도 닿을 수 있는**
계정·데이터 삭제 요청 URL 을 따로 적어야 한다. 앱 안의 "계정 지우기" 만으로는 이 요건을 채우지 못한다.

- 서버 백엔드가 없으므로 폼 제출이 아니라 **안내 + 메일 요청** 방식이다. 연락처는 방침의 문의처와 같은
  주소를 쓴다.
- Play 가 요구하는 내용: 앱 이름·개발자명, 앱에서 지우는 단계, 앱 없이 요청하는 방법, **지워지는 데이터와
  남는 데이터**, 처리 기간. 하나라도 빠지면 양식이 반려될 수 있다.
- 메일 요청은 개발자가 **콘솔에서 손으로** 처리한다(인증 계정·Firestore 문서·R2 객체). 페이지에 적은
  처리 기간(10일)을 지킬 수 있는 절차가 앱 저장소 쪽에 있어야 한다.
- 이 URL 도 처리방침 URL 처럼 한 번 등록하면 바꾸지 않는다.

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

- 사진·메모 등 **이용자 콘텐츠의 저장 방식 변경** — 여행첩 방침은 "사진은 리사이즈 사본만,
  EXIF 는 촬영 시각·회전만, 자동 백업 제외, 원본 미보관" 을 사실로 적고 있다.
  `PhotoStore` / `backup_rules.xml` / `data_extraction_rules.xml` 을 바꾸면 방침도 고친다
- 사진·여행 데이터의 동기화·업로드 도입 — 데이터 안전 양식의 "사용자 콘텐츠 = 수집 안 함" 이 뒤집힌다
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

### 여행첩 v3(보관·함께 편집)가 근거로 쓰는 값

되돌릴 수 없거나 코드에 있는 값이지만, 방침이 그대로 옮겨 적은 것이라 함께 적어 둔다.
정본은 trip_table 저장소의 `PRIVACY_POLICY_V3_DRAFT.md` 와 `DESIGN_SYNC_IMPLEMENTATION_PLAN.md` §7 이다.

| 값 | 현재 | 방침에서 근거로 쓰는 문장 |
|----|------|--------------------------|
| Firestore 데이터베이스 위치 | `asia-northeast3`(서울) — 생성 시 고정 | 국외 이전 표의 "대한민국 서울 리전" |
| R2 버킷 위치 힌트 | `APAC` — 힌트일 뿐 국가 보장 아님 | "아시아·태평양 지역 … 특정 국가를 보장하지 않습니다". **한 나라로 적지 않는다** |
| 사진 Worker 의 멤버십 캐시 | 최대 60초 | "확인 결과를 최대 1분간 다시 쓰므로 …" |
| 익명 계정 삭제 | 재인증 수단이 없어 거부될 수 있음 | "개인정보가 담기지 않은 익명 식별자가 인증 서비스에 남을 수 있습니다" |
| `CLOUD_ENABLED`(release) | v3 작성 시점에 **꺼짐** | v3 전체. 켜기 전에 v3 와 삭제 요청 페이지가 게시되어 있어야 한다 |

---

변경 시 문서의 **시행일을 갱신**하고, 이용자에게 불리한 변경은 시행 7일 전에 게시한다.
