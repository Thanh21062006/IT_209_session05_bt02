# Báo cáo Bài 2: Tái cấu trúc lịch sử commit bằng Interactive Rebase

## 1. Mục tiêu
- Sử dụng công cụ tương tác Interactive Rebase để chỉnh sửa lịch sử cục bộ.
- Gộp nhiều commit nhỏ lẻ (squash) thành một commit duy nhất có ý nghĩa.
- Đổi tên thông điệp commit (reword) và xóa bỏ một commit không cần thiết (drop).

## 2. Quá trình thực hiện
Trên nhánh làm việc, em đã tạo 4 commit rác/nhỏ lẻ như sau:
1. `feat: khoi tao module auth`
2. `fix typo`
3. `adds utility functions`
4. `add temp file for debug`

Để làm sạch lịch sử trước khi đẩy lên remote, em sử dụng lệnh Interactive Rebase lùi về 4 commit:
```bash
git rebase -i HEAD~4
```

Trong trình soạn thảo mở ra, em đã cấu hình các action cho từng commit như sau:
```
pick <hash1> feat: khoi tao module auth
squash <hash2> fix typo
squash <hash3> adds utility functions
drop <hash4> add temp file for debug
```
- **squash (s):** Gộp commit 2 và 3 vào commit 1.
- **drop (d):** Xóa bỏ hoàn toàn commit 4 (chứa file rác `temp.txt`).

Sau khi lưu và đóng file cấu hình, Git mở tiếp một cửa sổ để em soạn thảo lại thông điệp cho commit gộp (reword). Em đã đổi thông điệp thành:
`feat: hoan thien module authentication`

### Ảnh chụp giao diện cấu hình Interactive Rebase
*(Ảnh minh họa các lệnh pick, squash, drop)*

![ImgEx_Rebase]()

## 3. Kết quả lịch sử Commit
Sau khi hoàn tất rebase, lịch sử trở nên sạch sẽ, chỉ còn lại một commit duy nhất đại diện cho toàn bộ tính năng và không còn dấu vết của file `temp.txt`. Em kiểm tra bằng lệnh:
```bash
git log --oneline
```

### Ảnh chụp lịch sử Git Log sạch sẽ
*(Ảnh kết quả của lệnh git log --oneline)*

![ImgEx_GitLog]()
