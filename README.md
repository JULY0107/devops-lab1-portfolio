# DevOps Lab 1 — Portfolio + CI/CD

**Họ tên:** Nông Minh Hiếu
**MSSV:** DTC235180074
**Repo:** https://github.com/JULY0107/devops-lab1-portfolio
**Website live:** https://july0107.github.io/devops-lab1-portfolio/

## Mô tả
Website portfolio tĩnh (HTML/CSS) demo vòng đời DevOps:
`Code → git push main → GitHub Actions validate → Deploy sang gh-pages → Lighthouse audit → Live`.

## Cấu trúc
```
index.html / about.html / contact.html
assets/avatar.svg
.github/workflows/deploy.yml      → validate + deploy Pages
.github/workflows/lighthouse.yml  → audit Performance/Accessibility/SEO
.lighthouserc.json                 → cấu hình Lighthouse CI
COMPARISON.md                      → bảng so sánh DevOps vs Traditional
```

## Chạy local
Mở `index.html` bằng browser, hoặc:
```
npx serve .
```

## Pipeline
- Push lên `main` → job `build-and-deploy` chạy, publish `./` sang nhánh `gh-pages`.
- Job `lighthouse` chạy song song, upload report làm artifact.
- Bật Pages: Settings → Pages → Source: `gh-pages`.
