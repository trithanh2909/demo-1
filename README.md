# Bài tập nhóm: Tự cài đặt thuật toán băm MD5 bằng Python

> **Cảnh báo:** MD5 không còn an toàn cho các ứng dụng cần khả năng chống va chạm. Dự án này chỉ phục vụ học tập, nghiên cứu thuật toán và minh họa kiểm tra dữ liệu; không sử dụng để thiết kế cơ chế bảo mật mới.

## 1. Mục tiêu

Dự án được tổ chức thành hai tệp để thuận tiện cho việc nộp bài và trình diễn:

- `main.py`: chứa phần lõi MD5 tự cài đặt theo RFC 1321, chức năng băm văn bản/tệp, kiểm tra tính toàn vẹn, trace trạng thái và các bài tự kiểm thử cơ bản.
- `README.md`: hướng dẫn cài đặt, chạy chương trình và giải thích các giới hạn.

Phần lõi `md5()` tự thực hiện padding, chia khối 512 bit, xử lý 64 bước, cập nhật trạng thái 32 bit và xuất digest 128 bit. Hàm `hashlib.md5()` chỉ được gọi trong chức năng tự kiểm thử để đối chiếu kết quả, không được dùng thay cho lõi MD5.

## 2. Yêu cầu

- Python 3.10 trở lên.
- Không cần cài thư viện bên ngoài; chỉ dùng thư viện chuẩn Python.
- Chạy bằng Command Prompt, PowerShell hoặc Terminal.

Kiểm tra Python:

```bash
python --version
```

Trên Windows, nếu lệnh `python` không hoạt động nhưng `py` có sẵn, có thể thay `python` bằng `py` trong các lệnh bên dưới.

## 3. Chạy chương trình

Mở terminal tại thư mục chứa `main.py` và `README.md`, sau đó chạy:

```bash
python main.py
```

Menu cung cấp các lựa chọn:

1. Tính MD5 cho văn bản.
2. Tính MD5 cho một tệp.
3. Kiểm tra tính toàn vẹn của tệp bằng digest tham chiếu.
4. Hiển thị trace 8 bước đầu của MD5 với thông điệp `abc`.
5. Chạy bộ tự kiểm thử.
0. Thoát.

## 4. Chạy tự kiểm thử

Trong menu, chọn `5`. Hoặc chạy chương trình không tương tác bằng lệnh:

```bash
python main.py
```

Sau đó nhập `5` và kiểm tra kết quả ở cuối. Bộ tự kiểm thử hiện bao gồm:

- 7 test vector MD5 chuẩn theo RFC 1321.
- Kiểm thử các độ dài quanh ranh giới padding và khối dữ liệu.
- Kiểm thử văn bản tiếng Việt mã hóa UTF-8.
- Kiểm tra đầu vào không phải bytes.
- Kiểm tra trace có đủ 64 bước.
- Kiểm tra tệp nguyên bản khớp digest tham chiếu.
- Kiểm tra tệp đã thay đổi không khớp digest cũ.
- Kiểm tra digest tham chiếu sai định dạng.

Chỉ xem chương trình đạt khi tất cả các dòng kiểm tra hiện `[PASS]` và kết quả cuối ghi `OK`.

## 5. Kịch bản demo tính toàn vẹn tệp

1. Chạy `python main.py`.
2. Chọn `2`, nhập đường dẫn đến một tệp có sẵn; ghi lại digest được in ra.
3. Chọn `3`, nhập lại đường dẫn đó và dán digest vừa ghi. Kết quả mong đợi: `KHỚP`.
4. Sao chép tệp sang một tệp khác và sửa nội dung bản sao.
5. Chọn `3`, nhập đường dẫn bản sao và vẫn dùng digest được tính trước khi sửa. Kết quả mong đợi: `KHÔNG KHỚP`.

Nên sửa bản sao để tránh vô tình thay đổi tệp gốc cần sử dụng trong buổi thuyết trình.

## 6. Giới hạn cần nêu khi thuyết trình

- MD5 tạo digest 128 bit nhưng không còn phù hợp với các ứng dụng cần khả năng chống va chạm.
- Kiểm tra tính toàn vẹn chỉ có ý nghĩa khi digest tham chiếu đến từ một nguồn đáng tin cậy. Kẻ tấn công có thể thay cả tệp và digest thì phép so sánh đơn thuần không xác thực được nguồn gốc.
- Phiên bản demo này đọc toàn bộ tệp vào bộ nhớ trước khi băm, vì vậy phù hợp với tệp nhỏ và mục đích học tập, không tối ưu cho tệp rất lớn.
- Vượt qua bộ tự kiểm thử không chứng minh rằng thuật toán MD5 an toàn trước tấn công; nó chỉ là bằng chứng cho các trường hợp đã kiểm tra.

## 7. Tài liệu tham khảo kỹ thuật

1. R. Rivest, *The MD5 Message-Digest Algorithm*, RFC 1321, 1992: https://www.rfc-editor.org/rfc/rfc1321
2. S. Turner and L. Chen, *Updated Security Considerations for the MD5 Message-Digest and the HMAC-MD5 Algorithms*, RFC 6151, 2011: https://www.rfc-editor.org/rfc/rfc6151

## 8. Ghi nhận đóng góp và sử dụng công cụ

Nếu dự án được thực hiện theo nhóm, báo cáo hoặc phần trình bày nên ghi rõ người phụ trách từng phần, các nguồn kỹ thuật đã tham khảo và công cụ hỗ trợ đã sử dụng. Mỗi thành viên cần đọc và có khả năng giải thích phần code mình đóng góp. Chỉ ghi nhận những lần chạy kiểm thử và hoạt động review đã thực sự được thực hiện.
