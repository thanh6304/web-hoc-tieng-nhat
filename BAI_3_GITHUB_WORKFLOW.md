# BAI 3 - QUAN LY MA NGUON VOI GITHUB

Tai lieu nay thiet lap workflow GitHub theo dung yeu cau:

- Cau truc nhanh: `master` -> `develop` -> `feature/*`
- Dat ten nhanh ro rang: `feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>`
- Phan quyen: chi nhom truong duoc merge vao `develop`
- Phan biet ro nhanh cong ty va nhanh ca nhan

## 1. Quy uoc nhanh

### Nhanh cong ty (company branches)

- `master`: Nhanh san pham, chi chua ban on dinh da duoc kiem thu
- `develop`: Nhanh moi truong phat trien chung cua team

### Nhanh ca nhan (member branches)

- Mau bat buoc: `feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>`
- Vi du dung:
  - `feature/duc/homework-task1`
  - `feature/hao/jl46-ai-context`
  - `feature/thanh/payment-ipn-verify`

Luu y: Tat ca nhanh bat dau bang `feature/` deu la nhanh ca nhan, khong merge thang vao `master`.

## 2. Luong lam viec bat buoc

1. Nhom truong cap nhat `develop` tu `master` khi can release.
2. Moi thanh vien tao nhanh ca nhan tu `develop`.
3. Thanh vien code tren nhanh ca nhan va push len remote.
4. Thanh vien tao Pull Request (PR): `feature/...` -> `develop`.
5. Nhom truong review, approve, va merge PR vao `develop`.
6. Chi nhom truong tao PR `develop` -> `master` khi release.

## 3. Lenh Git ap dung ngay

### 3.1. Khoi tao nhanh chuan (neu chua co)

```powershell
git checkout master
git pull origin master
git checkout -b develop
git push -u origin develop
```

### 3.2. Thanh vien tao nhanh feature dung chuan

```powershell
git checkout develop
git pull origin develop
git checkout -b feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>
git push -u origin feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>
```

### 3.3. Lam viec va day code

```powershell
git add .
git commit -m "feat(task): mo ta ngan gon"
git push
```

### 3.4. Dong bo nhanh feature voi develop truoc khi tao PR

```powershell
git checkout develop
git pull origin develop
git checkout feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>
git rebase develop
git push --force-with-lease
```

## 4. Cau hinh quyen merge tren GitHub

Thiet lap Branch protection rules tren repo:

- Rule cho `develop`:
  - Require a pull request before merging
  - Require approvals: 1
  - Require review from Code Owners
  - Restrict who can push: chi nhom truong
- Rule cho `master`:
  - Require a pull request before merging
  - Require approvals: 1 hoac 2
  - Restrict who can push: chi nhom truong
  - Yeu cau build/test pass (neu da co CI)

## 5. Checklist danh cho thanh vien

- Nhanh dat dung mau `feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>`
- PR huong ve `develop`
- Da rebase voi `develop` moi nhat
- Mo ta ro task va pham vi thay doi
- Khong co file rac, khong commit `target/`, `logs/`

## 6. Ket luan phan biet nhanh

- Nhanh cong ty: `master`, `develop`
- Nhanh ca nhan: tat ca nhanh `feature/<thanh-vien>/...`

Nhu vay da co phan tach ro rang giua nhanh chinh cua cong ty va nhanh lam viec ca nhan cua tung thanh vien, dung voi yeu cau bai 3.