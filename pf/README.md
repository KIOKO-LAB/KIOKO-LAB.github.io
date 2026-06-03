# `/pf` — Path Finder smart router

`https://kiokolab.com/pf` 1개 URL로 모든 마케팅 채널을 통합. User-Agent 감지로 자동 라우팅.

## 동작

- **iPhone/iPad** → App Store (`id6757067771`)
- **Android** → `market://` 5ms 시도 → Play Store fallback
- **데스크톱·기타** → `/` (랜딩)
- 모든 쿼리 파라미터 passthrough. `utm_source`+`utm_medium`+`utm_campaign` 가 있으면 Play Store `referrer=` 로 자동 변환

## 채널별 권장 UTM

| 채널 | URL |
|---|---|
| 디시 갤러리 | `kiokolab.com/pf?utm_source=dcinside&utm_medium=community` |
| Reddit | `kiokolab.com/pf?utm_source=reddit&utm_medium=community&utm_campaign=r_puzzlegames` |
| TikTok bio | `kiokolab.com/pf?utm_source=tiktok&utm_medium=social` |
| YouTube 설명란 | `kiokolab.com/pf?utm_source=youtube&utm_medium=social&utm_content=shorts` |
| 이메일 시그니처 | `kiokolab.com/pf?utm_source=email&utm_medium=signature` |
| QR 코드 (오프라인) | `kiokolab.com/pf?utm_source=qr&utm_medium=offline` |

## 분석 확인

Google Play Console → **Acquisition reports → Tracked channels** 에서 `utm_source` 별 install 수 확인. iOS 는 App Store Connect → **App Analytics → Sources** (campaign tagging 활성 시).
