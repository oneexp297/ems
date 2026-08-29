# 비품 관리 — QR 스캐너

한나노텍 비품 관리 시스템에서 쓰는 QR 스캐너 한 장.

## 왜 앱 밖에 따로 있나

앱은 Google Apps Script 웹앱이라 화면이 `googleusercontent.com` 샌드박스
iframe 안에서 돈다. 카메라 권한은 상위 프레임이 `allow="camera"` 를 내려 줘야
하위 iframe 이 쓸 수 있는데, 그 상위 프레임은 구글이 만들고 우리가 고칠 수 없다.
그래서 아이폰에서는 **권한 창조차 뜨지 않은 채** `getUserMedia` 가 거부된다.

이 페이지는 GitHub Pages 에서 top-level 로 열리므로 그 제약이 없다.
QR 을 읽으면 앱 주소로 되돌아가며 값을 넘긴다.

## 쓰는 법

앱이 이렇게 부른다.

```
scan.html?ret=<앱 exec 주소>&kind=asset
```

- `ret` — 읽은 뒤 돌아갈 주소. **`script.google.com/macros/s/` 로 시작하는 것만 받는다.**
  안 그러면 이 페이지가 남의 피싱 링크를 이 도메인으로 세탁해 주는 공개 리디렉터가 된다.
- `kind` — `asset` 이면 비품, `user` 면 사용자. 화면 안내에만 쓴다.

읽은 값은 `ret` 에 `?qr=` 로 붙여 되돌린다. 앱 서버가 이미 그 길을 처리한다.

## 담긴 것

- 실시간 카메라 스캔 (html5-qrcode)
- 카메라가 안 되면 사진 한 장으로 읽기
- 안드로이드는 브라우저 내장 `BarcodeDetector` 를 먼저 쓴다

## 비밀은 없다

앱 주소만 들어간다. 그 주소는 익명 공개 배포라 누구나 열 수 있고,
실제 방어선은 앱 안의 PIN 로그인이다. 그래서 이 저장소는 공개해도 된다.

## Pages 켜기

저장소 Settings → Pages → Source 를 `main` 브랜치 루트로 두면
`https://<계정>.github.io/<저장소>/scan.html` 로 열린다.
