# CAU TRUC NHOM 4 NGUOI - WORKFLOW GITHUB (CHI TIET)

Tai lieu nay dung cho nhom 4 nguoi theo yeu cau bai 3:

- Cau truc nhanh: `master` -> `develop` -> `feature/*`
- Nhom truong la nguoi duy nhat review va merge vao `develop`
- Phan biet ro nhanh cong ty va nhanh ca nhan

## 1) Cau truc nhom de xuat

- Nguoi 1: Nhom truong (Leader)
- Nguoi 2: Thanh vien A
- Nguoi 3: Thanh vien B
- Nguoi 4: Thanh vien C

Khuyen nghi gan GitHub username ro rang:

- Leader: `@leader_username`
- Member A: `@member_a_username`
- Member B: `@member_b_username`
- Member C: `@member_c_username`

## 2) Phan tach nhanh ro rang

### Nhanh cong ty

- `master`: nhanh san pham on dinh
- `develop`: nhanh phat trien chung cua team

### Nhanh ca nhan (cho 4 nguoi)

Mau bat buoc:

`feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>`

Vi du cho nhom 4 nguoi:

- `feature/member-a/task1-login-ui`
- `feature/member-b/task2-payment-flow`
- `feature/member-c/task3-kanji-filter`
- `feature/leader/task4-review-rules`

## 3) Quy tac phan quyen merge

- Thanh vien chi duoc push len nhanh `feature/...` cua minh.
- Tat ca thay doi deu phai qua PR vao `develop`.
- Leader la nguoi duy nhat duyet va merge PR vao `develop`.
- Khong ai merge truc tiep vao `master`.

## 4) Luong lam viec chuan

1. Leader tao/cap nhat nhanh `develop`.
2. Moi thanh vien tao nhanh `feature/...` tu `develop`.
3. Thanh vien commit/push va tao PR vao `develop`.
4. Leader review theo checklist va merge.
5. Khi release, Leader tao PR `develop` -> `master`.

## 5) Lenh Git mau cho thanh vien

```powershell
git checkout develop
git pull origin develop
git checkout -b feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>
git push -u origin feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>
```

```powershell
git add .
git commit -m "feat(task): mo ta ngan gon"
git push
```

```powershell
git checkout develop
git pull origin develop
git checkout feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>
git rebase develop
git push --force-with-lease
```

## 6) Mau cau tao PR (copy dung ngay)

### Mau cau ngan gon

"Em gui PR tu nhanh `feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>` vao `develop` theo workflow bai 3. Em da rebase develop moi nhat, da tu test co ban, nho nhom truong review va merge."

### Mau cau day du

"Kinh gui nhom truong, em da hoan thanh task va tao PR tu nhanh `feature/<thanh-vien>/<ten-nhiem-vu>-<mo-ta>` vao `develop`. Thay doi gom: [liet ke ngan gon]. Em da pull/rebase tu `develop` moi nhat, tu kiem thu cac chuc nang lien quan va dinh kem bang chung test. Nho nhom truong review theo checklist va merge neu dat yeu cau."

## 7) Mau tieu de PR

`[TASK-<so>] <ten-nhiem-vu-ngan-gon> - <thanh-vien>`

Vi du:

- `[TASK-01] Login UI basic - member-a`
- `[TASK-02] Payment callback fix - member-b`

## 8) Checklist truoc khi bam Create PR

- [ ] Dung ten nhanh theo mau `feature/...`
- [ ] Target PR la `develop`
- [ ] Da rebase `develop` moi nhat
- [ ] Khong co file build/rac (`target/`, `logs/`)
- [ ] Co mo ta thay doi va bang chung test

## 9) Cau hinh GitHub khuyen nghi

- Branch protection cho `develop`:
  - Require pull request before merging
  - Require 1 approval
  - Require review from Code Owners
  - Restrict who can push/merge: Leader
- Branch protection cho `master`:
  - Require pull request before merging
  - Require approval (1-2)
  - Restrict who can push/merge: Leader

---

Neu dung dung tai lieu nay, nhom se dap ung day du yeu cau bai 3 ve cau truc nhanh, dat ten nhanh, phan quyen merge va phan biet nhanh cong ty/ca nhan.
