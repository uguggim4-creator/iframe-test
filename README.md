# class-ainspire

AInspire 모집 상세페이지 호스팅 repo.

- **도메인**: https://class.ainspire.co.kr
- **운영 방식**: 루트 `/`에 최신 페이지 하나만 배포
- **GitHub**: https://github.com/uguggim4-creator/iframe-test
- **호스팅**: Vercel (`iframe-test` 프로젝트)
- **DNS**: 가비아 `class` CNAME -> `e015c75382b1a660.vercel-dns-016.com.`

---

## 폴더 구조

```text
class-ainspire/
├─ index.html      # 최신 AInspire 상세페이지
├─ favicon.png     # 사이트 favicon
└─ README.md
```

루트 진입 시 리다이렉트 없이 바로 최신 상세페이지가 열립니다.

---

## 최신 페이지 교체

새 상세페이지 HTML을 받으면 루트 `index.html`을 교체합니다.

```powershell
cd F:\iframe-test
copy "C:\path\to\latest-page.html" index.html
git add index.html
git commit -m "Update latest landing page"
git push origin main
```

Vercel이 GitHub push를 감지해서 자동 배포합니다.

---

## 아임웹 상품 상세 iframe 코드

```html
<iframe
  src="https://class.ainspire.co.kr/"
  width="100%"
  height="8000"
  style="border:0;display:block;margin:0;padding:0;"
  loading="lazy"
  scrolling="no">
</iframe>
```

- `height`는 실제 페이지 길이에 맞춰 조정합니다.
- 페이지 안에는 iframe 높이 전달용 `postMessage` 코드가 포함되어 있습니다.

---

## 인프라 요약

| 구성 | 위치 | 비고 |
|---|---|---|
| 도메인 등록 | 가비아 `ainspire.co.kr` | |
| DNS | 가비아 DNS 관리 | `class` CNAME -> Vercel |
| Git remote | GitHub `uguggim4-creator/iframe-test` | Public repo |
| 호스팅/배포 | Vercel 프로젝트 `iframe-test` | GitHub 연동 자동 배포 |
| SSL | Vercel 자동 발급 | Let's Encrypt |

---

## 주의사항

- 기수별 폴더(`/4/`, `/5/` 등)는 만들지 않습니다.
- 루트 `/`가 항상 최신 상세페이지입니다.
- 아임웹에는 HTML을 직접 붙여넣지 말고 iframe으로 임베드합니다.
- `CNAME` 파일이나 `vercel.json`은 현재 구성에 필요하지 않습니다.
