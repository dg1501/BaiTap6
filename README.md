# Bài tập 6: Hệ quản trị CSDL
## Chủ đề: Câu lệnh Select
### Yêu cầu bài tập: 
Cho file sv_tnut.sql (1.6MB)
1. Hãy nêu các bước để import được dữ liệu trong sv_tnut.sql vào sql server của em
2. dữ liệu đầu vào là tên của sv; sđt; ngày, tháng, năm sinh của sinh viên (của sv đang làm bài tập này)
3. nhập sql để tìm xem có những sv nào trùng hoàn toàn ngày/tháng/năm với em?
4. nhập sql để tìm xem có những sv nào trùng ngày và tháng sinh với em?
5. nhập sql để tìm xem có những sv nào trùng tháng và năm sinh với em?
6. nhập sql để tìm xem có những sv nào trùng tên với em?
7. nhập sql để tìm xem có những sv nào trùng họ và tên đệm với em.
8. nhập sql để tìm xem có những sv nào có sđt sai khác chỉ 1 số so với sđt của em.
9. BẢNG SV CÓ HƠN 9000 ROWS, HÃY LIỆT KÊ TẤT CẢ CÁC SV NGÀNH KMT, SẮP XẾP THEO TÊN VÀ HỌ ĐỆM, KIỂU TIẾNG  VIỆT, GIẢI THÍCH.
10. HÃY NHẬP SQL ĐỂ LIỆT KÊ CÁC SV NỮ NGÀNH KMT CÓ TRONG BẢNG SV (TRÌNH BÀY QUÁ TRÌNH SUY NGHĨ VÀ GIẢI NHỮNG VỨNG MẮC)

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
- Tại cửa sổ New SQL, thêm đoạn code dưới và excute để tạo dữ liệu đầu vào.
```
DECLARE @masv VARCHAR(20) = 'K225480106093';
DECLARE @hodem NVARCHAR(50) = N'Nguyễn Đức';
DECLARE @ten NVARCHAR(20) = N'Dương';
DECLARE @ns DATE = '2004-01-15';
DECLARE @lop NVARCHAR(50) = N'K58KMT.01';
DECLARE @sdt VARCHAR(20) = '0396980922';

INSERT INTO SV (masv, hodem, ten, ns, lop, sdt)
VALUES (@masv, @hodem, @ten, @ns, @lop, @sdt);
```


