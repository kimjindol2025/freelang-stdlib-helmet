# freelang-stdlib-helmet

FreeLang v2 stdlib — npm **helmet** 완전 대체 구현

보안 HTTP 헤더를 자동으로 주입하는 미들웨어 모듈입니다.

## 주입 헤더 (기본 11개)

| 헤더 | 기본값 |
|------|--------|
| Content-Security-Policy | default-src 'self' |
| Cross-Origin-Embedder-Policy | require-corp |
| Cross-Origin-Opener-Policy | same-origin |
| Cross-Origin-Resource-Policy | same-origin |
| X-DNS-Prefetch-Control | off |
| X-Frame-Options | SAMEORIGIN |
| X-Powered-By | (제거) |
| Strict-Transport-Security | max-age=15552000; includeSubDomains |
| X-Content-Type-Options | nosniff |
| Referrer-Policy | no-referrer |
| X-XSS-Protection | 0 |

## 사용법

```fl
import "stdlib/helmet"

// 기본값 (권장)
app.use(helmet())

// 커스텀
app.use(helmetConfig({
  frameguard: "DENY",
  hsts: { maxAge: 31536000, includeSubDomains: true, preload: true }
}))

// 개별 적용
app.use(frameguard("DENY"))
app.use(hsts({ maxAge: 31536000, includeSubDomains: true, preload: false }))
```

## 구현 내용

- **struct**: `HSTSConfig`, `HelmetConfig`
- **핵심**: `helmet()`, `helmetConfig()`, `defaultHelmetConfig()`
- **개별 미들웨어**: 12개 (`contentSecurityPolicy`, `frameguard`, `hsts` 등)
- **프리셋**: `helmetStrict()`, `helmetApi()`
