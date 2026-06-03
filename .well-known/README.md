# `.well-known/` — Android App Links & iOS Universal Links

이 디렉토리는 `kiokolab.com/pf` 마케팅 링크를 **앱 설치된 사용자에게 직접 앱으로 열리게** 만들기 위한 association 파일들을 호스팅합니다.

## 파일 목록

| 파일 | 플랫폼 | 용도 |
|---|---|---|
| `assetlinks.json` | Android | Digital Asset Links — `com.puzzle_game.path_finder` 가 `kiokolab.com` URL 처리 권한을 위임받음 |
| `apple-app-site-association` | iOS | Universal Links — `com.puzzle-game.path-finder` 앱이 `/pf`, `/pf/*` 경로를 처리 (확장자 없음, Apple 요구사항) |

## GitHub Pages 호스팅 메모

- 리포 루트의 `.nojekyll` 덕분에 dot-prefix 디렉토리(`.well-known/`)도 서빙됩니다.
- `apple-app-site-association` 은 **Content-Type 이 `application/json`** 이어야 iOS swcd 가 받아들입니다. GitHub Pages 는 확장자 없는 파일에 `application/octet-stream` 을 줄 수 있으니 라이브 후 반드시 헤더 검증 필요.
  - 만약 octet-stream 으로 나오면 fallback: Cloudflare/Netlify 프록시 또는 Worker 로 헤더 override.

## 운영자가 채워야 할 placeholder

작업 시점에는 비워뒀습니다. 채우고 push 하면 라이브.

- `assetlinks.json` → `<<SHA256_FINGERPRINT_REPLACE_ME>>`
  - 위치: Play Console → 설정 → 앱 무결성 → 앱 서명 키 인증서 → SHA-256 인증서 지문 복사
  - 형식: `XX:XX:XX:...` (95자, 콜론 포함)
  - debug + release 등 복수 키는 array 에 한 줄씩 추가
- `apple-app-site-association` → `<<APPLE_TEAM_ID_REPLACE_ME>>` (2곳)
  - 위치: [Apple Developer 계정 멤버십 페이지](https://developer.apple.com/account) → Team ID (10자 영숫자)

## 검증 명령 (push 후)

### Android assetlinks
```bash
curl -s https://kiokolab.com/.well-known/assetlinks.json | python3 -m json.tool
```

Google 공식 verifier:
```
https://developers.google.com/digital-asset-links/tools/generator
```
- Hosting site: `https://kiokolab.com`
- Package name: `com.puzzle_game.path_finder`
- SHA-256: 채운 값

### iOS AASA
```bash
curl -I https://kiokolab.com/.well-known/apple-app-site-association
```
- `Content-Type` 값 확인 (`application/json` 이어야 OK, `application/octet-stream` 이면 위 메모 참고)

Apple 공식 validator:
```
https://branch.io/resources/aasa-validator/?domain=kiokolab.com
```
또는
```
https://app-site-association.cdn-apple.com/a/v1/kiokolab.com
```
(CDN 캐시 — 최초 라이브 후 ~24h 지연 가능)
