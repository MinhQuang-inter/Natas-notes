# prokyurem

## Natas level 9

---

## 📌 Nội dung đầu bài

- Khi đăng nhập vào **natas9** bạn sẽ chỉ thấy có ô `Find words containing`.
  -> Màn này chúng ta cần tìm đoạn mã để điền vào ô trống đó để nhận được password.

- Ta nhìn bên cạnh thì thấy dòng **View sourcecode**.
- Khi ấn vào ta sẽ thấy đoạn code PHP sau (gợi ý).

```php
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
```

- Đoạn code PHP ở trên cho ta biết rằng:
  1. Nhận input từ người dùng
     Code lấy tham số needle từ $\_REQUEST (nghĩa là nhận được từ cả GET lẫn POST).
     Nếu tồn tại thì gán vào biến $key.
  2. Chạy lệnh hệ thống.
     `passthru("grep -i $key dictionary.txt");`
     Ở đây nó sẽ chạy:
     grep -i <giá trị của &key> dictionary.txt.
  3. Điểm yếu (Vulnerable Point)
     Ở đây không có lọc input $key được đưa thẳng vào command line. Nghĩa là ta có thể chèn thêm lệnh khác vào. Đây là lỗ hổng `Command Injection`.

---

## 🔑 Cách bypass

- Mật khẩu của các màn trong natas thường lưu ở `file /etc/natas_webpass/...`
  -> Mật khẩu của màn 10 sẽ nằm ở `file /etc/natas_webpass/natas10`
  -> Ta sẽ thay thế `&key = cat /etc/natas_webpass/natas10`, nhưng vì ở đằng trước &key có đoạn `grep -i` nên ta cần phải cho dấu **;** hoặc dấu **|** ở giữa để liên kết 2 câu lệnh
- Hoàn chỉnh câu lệnh sẽ thực hiện là `grep -i | cat /etc/natas_webpass/natas10 dictionary.txt`
- Như vậy ta chỉ cần điền đoạn lệnh `| cat /etc/natas_webpass/natas10` vào trong ô trống là ta sẽ nhận được mật khẩu hoặc ta có thể thay thể hẳn đoạn url thành `http://natas9.natas.labs.overthewire.org/?needle=; cat /etc/natas_webpass/natas10` là ta sẽ nhận được mật khẩu

**✅ Password: `t7I5VHvpa14sJTUGV0cbEsbYfFP2dmOu`**
