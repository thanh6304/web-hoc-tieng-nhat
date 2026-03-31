# 🎯 Hướng Dẫn Làm Việc - Người A (Jira + GitHub Workflow)

## 📋 Danh Sách Task Gán Cho Người A

Từ Jira board hiện tại, Người A nhận các task:
- [ ] **WHTN-13**: Thanh toán Momo | To Do | Medium
- [ ] **WHTN-7**: Testing & QA | To Do
- [ ] **WHTN-4**: AI Features | To Do
- [ ] Và các task khác được assign...

---

## 🚀 Quy Trình Làm Việc - Từng Bước

### **Bước 1: Nhận Task Từ Jira**
1. Vào Jira, click vào task (VD: WHTN-13 Thanh toán Momo)
2. Click nút **"Start work"** → status chuyển sang **"IN PROGRESS"**
3. Copy lại **Task ID** (VD: `WHTN-13`)

---

### **Bước 2: Tạo Nhánh Feature Chuẩn**

#### **2a. Cú Pháp Tên Nhánh** (Bắt buộc tuân thủ)
```
feature/[TASK-ID]/[mô-tả-ngắn-bằng-tiếng-anh]
```

#### **2b. Ví Dụ Cụ Thể - Task WHTN-13**
```bash
# Terminal: Tạo nhánh mới từ develop
git checkout develop
git pull origin develop

# Tạo nhánh feature cho WHTN-13
git checkout -b feature/WHTN-13/momo-payment
# hoặc dài hơn
git checkout -b feature/WHTN-13/implement-momo-payment-system

# Đẩy nhánh lên GitHub để nhóm thấy bạn đang làm
git push origin feature/WHTN-13/momo-payment
```

#### **2c. Danh Sách Nhánh Template Cho Người A**
Sao chép cú pháp này cho task của bạn:

| Task Jira | Tên Nhánh (Copy Ngay) | Mô Tả |
|-----------|------------------|-------|
| WHTN-13 | `feature/WHTN-13/momo-payment` | Thanh toán Momo |
| WHTN-7 | `feature/WHTN-7/testing-qa` | Testing & QA workflow |
| WHTN-4 | `feature/WHTN-4/ai-features` | AI Features |

---

### **Bước 3: Viết Commit Message Chuẩn**

#### **3a. Format Commit**
```
[TASK-ID] Tiêu đề commit (50 ký tự)

Mô tả chi tiết (nếu cần):
- Cái gì đã thay đổi?
- Tại sao phải thay đổi?
- Impact của PR?
```

#### **3b. Ví Dụ Commit Cho WHTN-13**
```bash
git add .
git commit -m "[WHTN-13] Add Momo payment integration

- Implement MomoPaymentService with retry logic
- Add unit tests for payment processing
- Update application.yml with Momo API config
- Tested with test account, ready for review"
```

#### **3c. Commit Messages Tối Thiểu (Phải Có Task ID)**
```bash
git commit -m "[WHTN-13] Add Momo payment gateway"
git commit -m "[WHTN-13] Fix payment callback validation"
git commit -m "[WHTN-13] Update Momo API configuration"
```

---

### **Bước 4: Push Code Lên Nhánh Feature**

```bash
# Push nhánh lên GitHub
git push origin feature/WHTN-13/momo-payment

# Nếu có conflict, giải quyết rồi:
git push origin feature/WHTN-13/momo-payment --force-with-lease
```

---

### **Bước 5: Tạo Pull Request (PR) - Chi Tiết**

#### **5a. Login GitHub → Repo → Pull Requests**
1. Click **"New Pull Request"**
2. Set:
   - **Base**: `develop` (nhánh mục tiêu)
   - **Compare**: `feature/WHTN-13/momo-payment` (nhánh của Người A)

#### **5b. Tiêu Đề PR (Bắt Buộc)**
```
[WHTN-13] Implement Momo payment system
```
Hoặc:
```
[WHTN-13] Add MoMo Payment Integration
```

#### **5c. Nội Dung PR (Copy Template Dưới Đây)**

```markdown
## 🎯 Mô Tả
Implement Momo payment gateway integration cho phép user thanh toán khóa học qua MoMo.

## 📝 Task Jira
- Jira Issue: [WHTN-13](https://jira-link.com/browse/WHTN-13)

## ✅ Checklist Trước Khi Submit
- [x] Code follows project style guidelines
- [x] Ran local tests - all passing
- [x] Added unit tests for new logic
- [x] Updated relevant documentation
- [x] No breaking changes
- [x] Backward compatible
- [x] Tested in local environment (application-local.yml)

## 🔍 Kiểm Tra Cụ Thể
- [x] MomoPaymentService hoạt động đúng
- [x] Callback từ Momo server được xử lý
- [x] Error handling & retry logic hoạt động
- [x] Unit tests cover main scenarios
- [x] Integration tests passed

## 📸 Screenshots / Video
(Nếu có UI changes)
- Local testing result: ![screenshot.png]

## 🚀 Deployment Notes
- Cần setup Momo API credentials trong environment variables
- `MOMO_PARTNER_CODE=` 
- `MOMO_ACCESS_KEY=`
- `MOMO_SECRET_KEY=`

## 🔗 Related Issues
- Closes WHTN-13
```

#### **5d. Bấm "Create Pull Request"**
- Tự động tag nhóm trưởng (CODEOWNERS)
- Mô tả task ID trong PR
- Chờ nhóm trưởng review + approve

---

### **Bước 6: Code Review & Fix**

Khi nhóm trưởng hoặc code reviewer yêu cầu sửa:

```bash
# Sửa code theo feedback
# Hoặc update file cần thiết

# Commit thay đổi
git add .
git commit -m "[WHTN-13] Address review feedback: fix validation logic"

# Push lên cùng PR
git push origin feature/WHTN-13/momo-payment
```

PR sẽ **tự động update** với commit mới này.

---

### **Bước 7: Merge - Chỉ Nhóm Trưởng Được Phép**

**Khi nhóm trưởng duyệt:**
1. Click **"Squash and merge"** hoặc **"Create a merge commit"**
2. Nhánh feature tự động xóa sau merge
3. Task WHTN-13 trên Jira chuyển sang **"DONE"**

---

## 📌 Checklist Hoàn Thiện Task

Trước khi bấm "Create PR", Người A **PHẢI** check:

- [ ] Nhánh đúng tên: `feature/WHTN-13/momo-payment`
- [ ] Base branch là `develop` (không phải `master`)
- [ ] Commit messages có `[WHTN-13]` ở đầu
- [ ] Tất cả tests local pass
- [ ] Không có merge conflicts
- [ ] PR title có `[WHTN-13]`
- [ ] PR description điền đầy đủ (dùng template)
- [ ] Link Jira issue trong PR
- [ ] Không commit file không cần (`.class`, `target/`, `.env` riêng tư)

---

## 🛑 Lỗi Thường Gặp & Cách Khắc Phục

### **Lỗi 1: Push Sai Base Branch (→ master)**
```bash
# ❌ Sai - đã push lên master
git push origin feature/WHTN-13/momo-payment

# ✅ Sửa: Reset master về commit cũ
git reset --hard origin/master
git checkout feature/WHTN-13/momo-payment
git push origin feature/WHTN-13/momo-payment
```

### **Lỗi 2: Merge Conflict Trước Khi PR**
```bash
# Cập nhật develop mới nhất
git fetch origin
git rebase origin/develop

# Giải quyết conflict trong editor
# Sau đó:
git add .
git rebase --continue
git push origin feature/WHTN-13/momo-payment --force-with-lease
```

### **Lỗi 3: Quên Thêm Task ID Vào Commit**
```bash
# Sửa commit cuối cùng
git commit --amend -m "[WHTN-13] Original message"
git push origin feature/WHTN-13/momo-payment --force-with-lease
```

### **Lỗi 4: Nhánh Cũ Không Xóa**
```bash
# Xóa nhánh local đã merge
git branch -d feature/WHTN-13/momo-payment

# Xóa trên GitHub (sau khi merge)
git push origin --delete feature/WHTN-13/momo-payment
```

---

## 🎓 Ví Dụ Thực Tế - Full Workflow WHTN-13

```bash
# 1. Nhận task WHTN-13 từ Jira, click "Start work"

# 2. Tạo nhánh
git checkout develop
git pull origin develop
git checkout -b feature/WHTN-13/momo-payment

# 3. Làm việc trên code
# ... edit files ...
# src/main/java/com/japaneseLearning/service/MomoPaymentService.java
# src/test/java/com/japaneseLearning/service/MomoPaymentServiceTest.java

# 4. Run local tests
mvn clean test -DskipTests=false

# 5. Commit
git add .
git commit -m "[WHTN-13] Implement MoMo payment integration

- Add MomoPaymentService with async payment processing
- Implement callback handler for transaction status
- Add unit tests (100% coverage)
- Config: MOMO_PARTNER_CODE, MOMO_ACCESS_KEY required in .env"

# 6. Push
git push origin feature/WHTN-13/momo-payment

# 7. Tạo PR trên GitHub
# - Base: develop
# - Compare: feature/WHTN-13/momo-payment
# - Title: [WHTN-13] Implement MoMo payment system
# - Description: (copy template ở mục 5c)

# 8. Chờ Review từ nhóm trưởng...

# 9. Nếu có feedback, sửa code:
git add .
git commit -m "[WHTN-13] Fix payment validation per review feedback"
git push origin feature/WHTN-13/momo-payment

# 10. Merge thành công! ✅
# -> Nhánh tự xóa, task WHTN-13 → DONE trên Jira
```

---

## 📞 Liên Hệ / Hỏi Đáp

- **Git Issue**: Hỏi nhóm trưởng hoặc leader
- **Code Issue**: Discuss trong PR comments
- **Jira Issue**: Comment trong task WHTN-13

---

**Version**: 1.0  
**Last Updated**: 31/03/2026  
**Người Lập**: Team Leader  
**Áp Dụng Cho**: Nhóm 4 Người - Bài 3 GitHub Workflow
