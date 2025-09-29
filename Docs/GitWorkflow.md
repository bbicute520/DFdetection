# 🚀 Git Workflow cho Nhóm  

Hướng dẫn chi tiết cách làm việc với repo Git trong nhóm để code đồng bộ, tránh conflict và giữ repo sạch sẽ.  

---

## 🌳 Cấu trúc nhánh  
- **`main`** → code ổn định, release (❌ không ai push trực tiếp).  
- **`dev`** → tập hợp code đã review, ổn định trước khi lên `main`.  
- **`feature/<tên>`** → nhánh riêng cho từng task/tính năng.  
- (Tuỳ dự án có thể có thêm `hotfix/`, `release/`).  

📌 **Nguyên tắc**:  
- Luôn tạo nhánh mới từ `dev`.  
- Không code trực tiếp trên `main` hoặc `dev`.  

---

## ⚡ Quy trình làm việc  
# 1. Đồng bộ code mới nhất  
git checkout dev  
git pull origin dev  
# 2. Tạo nhánh mới cho task  
git checkout -b feature/<task-name>  
Ví dụ: feature/login-ui, fix/api-timeout  
# 3. Commit code  
-Commit nhỏ, rõ ràng.  
-Sử dụng Conventional Commits:  
    + feat: thêm tính năng  
    + fix: sửa bug  
    + refactor: cải thiện code  
    + docs: cập nhật tài liệu  
    + test: thêm/sửa test  
    + chore: việc phụ (config, build,...)  
git add .  
git commit -m "feat: thêm giao diện login"  
# 4. Push nhánh  
git push origin feature/<task-name>  
# 5. Tạo Pull Request (PR)  
- Tạo PR từ feature/... → dev.  
- Viết mô tả thay đổi (làm gì, ảnh hưởng gì).  
- Nhờ người khác review trước khi merge.  
# 6. Merge dev → main  
- Chỉ leader merge.  
- Chỉ merge khi dev đã ổn định, test đầy đủ.  
- Merge bằng Squash/Rebase để lịch sử gọn.  
  
🔑 Lưu ý quan trọng  
- Luôn pull trước khi code  
    git pull --rebase origin dev  
- Không commit file rác → dùng .gitignore.  
- Không force-push lên nhánh chung (dev, main).  
- Đặt tên branch rõ ràng → feature/login-ui, fix/api-timeout.  
- Review kỹ trước khi merge.  
  
🛠 Một số lệnh hữu ích  
# Xem nhánh hiện tại  
git branch  
  
# Xoá nhánh sau khi merge  
git branch -d feature/<task>  
git push origin --delete feature/<task>  
  
# Undo commit (chưa push)  
git reset --soft HEAD~1  
  
# Revert commit (đã push)  
git revert <commit_id>  
  
✅ Checklist trước khi push  
 Đã pull/rebase code mới nhất từ dev.  
 Không commit file rác (node_modules, __pycache__, .env...).  
 Commit message rõ ràng, có prefix (feat, fix, docs...).  
 Code chạy được, không lỗi build.  
 Viết thêm test/tài liệu nếu cần.  