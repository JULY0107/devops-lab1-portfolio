# Bảng So sánh: DevOps vs Traditional + Workflow (CDR 1.2 / 1.3)

**Sinh viên:** Nông Minh Hiếu — DTC235180074

## 1. Bảng so sánh

| Tiêu chí | Traditional (truyền thống) | DevOps |
|---|---|---|
| Quy trình | Code → test tay → copy file lên server bằng tay | Code → push → CI tự build/test/deploy |
| Tốc độ release | Chậm, theo đợt (tuần/tháng), dễ dồn ứ | Nhanh, nhiều lần/ngày, thay đổi nhỏ |
| Rủi ro deploy | Cao (sai tay, quên file, downtime) | Thấp (pipeline chuẩn, rollback nhanh) |
| Phối hợp Dev–Ops | Tách biệt, ném qua tường | Chung pipeline, chung trách nhiệm |
| Kiểm thử | Cuối vòng đời, thủ công | Tự động mỗi commit (validate, Lighthouse) |
| Phản hồi lỗi | Phát hiện muộn khi đã live | Phát hiện sớm ngay trong Actions log |
| Ví dụ lab này | Sửa `index.html` rồi FTP tay lên host | `git push origin main` → Actions deploy → `*.github.io` tự cập nhật |

## 2. Workflow DevOps trong Lab 1

```
Dev (local)
  │  git add / commit
  ▼
git push origin main
  │
  ▼
GitHub Actions (on: push → main)
  ├── Job build-and-deploy
  │     ├── Checkout code
  │     ├── Validate HTML (index/about/contact + avatar)
  │     └── peaceiris/actions-gh-pages → publish ./ sang nhánh gh-pages
  └── Job lighthouse (song song)
        ├── Setup Node + LHCI
        ├── Audit staticDistDir=./ (Performance, Accessibility, SEO)
        └── Upload report (artifact + temporary-public-storage)
  │
  ▼
GitHub Pages (nhánh gh-pages) → https://july0107.github.io/devops-lab1-portfolio/
  │
  ▼
Kiểm tra: mở URL → thấy portfolio (nếu sửa code, pipeline chạy lại, web update)
```

## 3. Hiểu vòng đời DevOps (CDR 1.3)
Plan → Code → Build → Test (validate + Lighthouse) → Release (gh-pages) → Deploy (Pages) → Operate/Monitor (Actions log + kiểm tra URL) → lặp lại mỗi push.
