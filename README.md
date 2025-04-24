# BÀI TẬP 6: HỆ QUẢN TRỊ CSDL
## Chủ đề: Câu lệnh SELECT
### Yêu cầu bài tập: 
Cho file sv_tnut.sql (1.6MB).
1. Hãy nêu các bước để import được dữ liệu trong sv_tnut.sql vào sql server của em. 
2. dữ liệu đầu vào là tên của sv; sđt; ngày, tháng, năm sinh của sinh viên (của sv đang làm bài tập này). 
3. nhập sql để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm với em?
4. nhập sql để tìm xem có những sv nào trùng ngày và tháng sinh với em?
5. nhập sql để tìm xem có những sv nào trùng tháng và năm sinh với em?
6. nhập sql để tìm xem có những sv nào trùng tên với em?
7. nhập sql để tìm xem có những sv nào trùng họ và tên đệm với em?
8. nhập sql để tìm xem có những sv nào có sđt sai khác chỉ 1 số so với sđt của em?
9. BẢNG SV CÓ HƠN 9000 ROWS, HÃY LIỆT KÊ TẤT CẢ CÁC SV NGÀNH KMT, SẮP XẾP THEO TÊN VÀ HỌ ĐỆM, KIỂU TIẾNG  VIỆT, GIẢI THÍCH?
10. HÃY NHẬP SQL ĐỂ LIỆT KÊ CÁC SV NỮ NGÀNH KMT CÓ TRONG BẢNG SV (TRÌNH BÀY QUÁ TRÌNH SUY NGHĨ VÀ GIẢI NHỮNG VỨNG MẮC)?

## BÀI LÀM
### TIẾN HÀNH TẠO DATABASE + TẠO BẢNG + DỮ LIỆU DEMO CHO BẢNG ( YÊU CẦU 1 CỦA ĐỀ BÀI ).
1. Tạo New Database.
![Untitled](https://github.com/user-attachments/assets/da8c3c70-2a77-4ec8-8b83-2e1e5bbe86a0)

2. Sau khi tạo Database -> Chọn New query để tiến hành tạo bảng và thêm dữ liệu đề mô vào bảng
![Untitled](https://github.com/user-attachments/assets/eefbb20a-7cd9-47d7-b412-210564e4a402)

3. Tiến hành tạo bảng + thêm dữ liệu cho bảng ( dựa vào file sv_tnut.sql )
![image](https://github.com/user-attachments/assets/94cb69bc-25eb-4a74-a80e-3a13fc4c4d07)

-3.1. Tạo bảng SV ( Bôi đen phần code tạo bảng và chọn EXCUTE để chạy code. Lưu ý: Muốn chạy code phần nào thì bôi đen phần đó, không nên chạy tất cả, vì sẽ xảy ra lỗi ).
![Untitled](https://github.com/user-attachments/assets/3d8b576f-b285-4257-8352-7767372c679f)

-3.2. Thêm dữ liệu cho bảng SV
![Untitled](https://github.com/user-attachments/assets/fef4302b-3bd9-4942-8663-5550f7b99ef8)

### THỰC HIỆN CÁC YÊU CẦU TỪ 2->9 
1. Dữ liệu đầu vào là tên của sv; sđt; ngày, tháng, năm sinh của sinh viên (của sv đang làm bài tập này).
```
masv : K225480106093
hodem: Nguyễn Đức
ten  : Dương
ns   : 2004-01-15
sđt  : 0396980922
```

2. Nhập SQL để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm với em?
```
SELECT * FROM SV
WHERE ns = '2004-01-15';
```
![Untitled](https://github.com/user-attachments/assets/2f55e06d-cc0b-4042-9b6e-4f538075d448)

3. Nhập SQL để tìm xem có những sv nào trùng ngày và tháng sinh với em?
```
SELECT * FROM SV
WHERE DAY(ns) = 15 AND MONTH(ns) = 01;
```
![image](https://github.com/user-attachments/assets/38e48f65-ad81-4723-9ac4-1f743c6b4281)

4. Nhập SQL để tìm xem có những sv nào trùng tháng và năm sinh với em?
```
SELECT * FROM SV
WHERE MONTH(ns) = 01 AND YEAR(ns) = 2004;
```
![image](https://github.com/user-attachments/assets/ff555cb7-b991-4a8c-bfb4-c53fe9471d74)

5. Nhập SQL để tìm xem có những sv nào trùng tên với em?
```
SELECT * FROM SV
WHERE ten = N'Dương';
```
![image](https://github.com/user-attachments/assets/d9271f2e-bf48-4ddf-94f5-ebe74d713243)

6. Nhập SQL để tìm xem có những sv nào trùng họ và tên đệm với em?
```
SELECT * FROM SV
WHERE hodem = N'Nguyễn Đức';
```
![Untitled](https://github.com/user-attachments/assets/f6351dd8-ef92-4a71-a79e-a48970a0ca0e)

7. Nhập sql để tìm xem có những sv nào có sđt sai khác chỉ 1 số so với sđt của em?
```
SELECT * FROM SV
WHERE LEN(sdt) = LEN('0396980922')
AND (
    SELECT COUNT(*) 
    FROM (VALUES (1),(2),(3),(4),(5),(6),(7),(8),(9),(10)) AS T(n)
    WHERE SUBSTRING(sdt, T.n, 1) <> SUBSTRING('0396980922', T.n, 1)
) = 1;
```
![Untitled](https://github.com/user-attachments/assets/ffea5731-dee3-4b48-bdd0-b494ebec40d9)

8. BẢNG SV CÓ HƠN 9000 ROWS, HÃY LIỆT KÊ TẤT CẢ CÁC SV NGÀNH KMT, SẮP XẾP THEO TÊN VÀ HỌ ĐỆM, KIỂU TIẾNG  VIỆT, GIẢI THÍCH?
```
SELECT masv, hodem, ten, ns, lop, sdt
FROM SV
WHERE lop LIKE N'%KMT%'
ORDER BY 
    lop COLLATE Vietnamese_CI_AS,
    ten COLLATE Vietnamese_CI_AS,
    hodem COLLATE Vietnamese_CI_AS;
```
![Untitled](https://github.com/user-attachments/assets/49af3877-6657-4499-a818-661c8ad84b29)

- 8.1. Giải thích :
+ SELECT .... : Tên các cột muốn hiển thị
+ FROM ...    : Lấy dữ liệu từ bảng SV
+ WHERE...    : Lọc ra những sinh viên thuộc lớp KMT
+ OREDER BY   : Là chuẩn sắp xếp theo chữ hoa, chữ thường, theo bảng chũ cái a,ă,â,... . Nếu không dùng COLLATE thì sẽ sắp xếp theo chuẩn Tiếng Anh.

9. HÃY NHẬP SQL ĐỂ LIỆT KÊ CÁC SV NỮ NGÀNH KMT CÓ TRONG BẢNG SV (TRÌNH BÀY QUÁ TRÌNH SUY NGHĨ VÀ GIẢI NHỮNG VỨNG MẮC)?
- Vì bảng SV không có trường ' Giới tính ' nên việc xác định sinh viên này có phải là nữ hay không là 1 việc khó. Vì vậy không thể chắc chắc 100% sinh viên này là nữ, vậy nên chỉ có thể dựa vào tên để lọc.
- Sử dụng lệnh để lọc những sinh viên có tên nữ phổ biến như là: Anh, Thảo, Lan, Hoa,...
- Việc lọc theo phán đoán như vậy sẽ xảy ra việc xót dữ liệu, tức là sẽ có những sinh viên là nữ nhưng do trong quá trình truy vấn không đề cập đến tên của sinh viên đó.
- Ý tưởng:
+ Đầu tiên sử dụng câu điều kiện lop LIKE N'%KMT%' để lọc những sinh viên lớp KMT.
+ Sau đó tiến hành sử dụng câu lệnh ' AND ten IN ( tên sinh viên nữ mà bạn phán đoán VD: N'Hương' ) '.
+ Độ chính xác sẽ phụ thuộc vào độ chi tiết cũng như đầy đủ của phần tên sinh viên mà bạn khai báo.
```
SELECT masv, hodem, ten, ns, lop, sdt
FROM SV
WHERE lop LIKE N'%KMT%'
  AND ten IN (N'Anh', N'Lan', N'Thảo', N'Hương', N'Linh', N'Trang', N'Phương', N'Yến', N'Huyền', N'Nhung', N'Ngọc', N'Ánh', N'Hoa', N'Hoài')
ORDER BY 
    lop COLLATE Vietnamese_CI_AS_KS_WS,
    ten COLLATE Vietnamese_CI_AS_KS_WS,
    hodem COLLATE Vietnamese_CI_AS_KS_WS;
```
![Untitled](https://github.com/user-attachments/assets/29d462fb-3c27-4d67-aa8f-e24a9ab56e0a)

- Những vướng mắc: Việc sắp xếp theo kiểu tiếng việt tức theo trình tự bảng chữ cái tiếng việt rất khó khắn, do có những tên chứa ký tự đặc biệt như ' Ánh, Ân, ...' . Lý do có thể là SQL Server chỉ hỗ trợ 1 phần chuẩn sắp xếp Tiếng Việt
