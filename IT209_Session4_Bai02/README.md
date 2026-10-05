# Session 04 - Bài 2: Quản lý nhánh và Giải quyết xung đột (Merge Conflict)

## 1. Mục tiêu
- Tạo mới và di chuyển linh hoạt giữa các nhánh (branch) cục bộ.
- Cố ý tạo ra xung đột gộp nhánh (Merge Conflict) và xử lý xung đột thủ công.
- Hoàn thành commit gộp nhánh và hiểu cơ chế 3-Way Merge.

## 2. Các bước thực hiện

### Bước 1: Tạo nhánh `feature-update` và commit thay đổi trên đó
```bash
git checkout -b feature-update
```

Chỉnh sửa file `README.md` trên nhánh `feature-update`:
```bash
echo "Feature: Updated by feature-update branch" > README.md
git add README.md
git commit -m "feat: update README from feature-update branch"
```

### Bước 2: Quay lại nhánh `main` và commit thay đổi cùng dòng
```bash
git checkout main
```

Chỉnh sửa file `README.md` trên nhánh `main` (cùng dòng để gây xung đột):
```bash
echo "Main: Updated by main branch" > README.md
git add README.md
git commit -m "fix: update README from main branch"
```

### Bước 3: Gộp nhánh `feature-update` vào `main` (gây xung đột)
```bash
git merge feature-update
```

**Kết quả:** Git báo xung đột:
```text
Auto-merging README.md
CONFLICT (content): Merge conflict in README.md
Automatic merge failed; fix conflicts and then commit the result.
```

### Bước 4: Giải quyết xung đột thủ công
Mở file `README.md`, nội dung xung đột:
```text
<<<<<<< HEAD
Main: Updated by main branch
=======
Feature: Updated by feature-update branch
>>>>>>> feature-update
```

Xử lý thủ công: xóa các ký hiệu đánh dấu xung đột và giữ lại nội dung hợp nhất:
```text
Main & Feature: Combined update from both main and feature-update branches
```

### Bước 5: Commit gộp nhánh
```bash
git add README.md
git commit -m "merge: resolve conflict between main and feature-update"
```

## 3. File README.md sau khi giải quyết xung đột

```text
Main & Feature: Combined update from both main and feature-update branches
```

## 4. Kết quả kiểm tra

### Lịch sử commit dạng đồ thị nhánh:
```bash
git log --graph --oneline
```
```text
*   e5f6g7h (HEAD -> main) merge: resolve conflict between main and feature-update
|\
| * c3d4e5f (feature-update) feat: update README from feature-update branch
* | b2c3d4e fix: update README from main branch
|/
* a1b2c3d Initial commit: add README.md for DevOps project
```

Kết quả cho thấy nhánh `feature-update` đã tách ra từ `main`, sau đó gộp lại với một **merge commit** có 2 nhánh tổ tiên (2 parent commits).
