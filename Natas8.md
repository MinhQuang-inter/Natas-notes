# prokyurem

## Natas level 8

---

## 📌 Nội dung đầu bài

- Khi đăng nhập vào **natas8** bạn sẽ chỉ thấy có ô `input secret`.  
  → Màn này muốn chúng ta tìm ra **secret** để điền vào ô đó, khi đó ta sẽ tìm được password cho màn tiếp theo.

- Ta nhìn bên cạnh thì sẽ thấy được dòng **view sourcecode**.
- Khi ấn vào sẽ thấy đoạn code PHP sau (gợi ý):

```php
$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
        print "Access granted. The password for natas9 is <censored>";
    } else {
        print "Wrong secret";
    }
}
```

- Đoạn code trên thực hiện 3 bước:
  1. `base64_encode($secret)` → mã hóa chuỗi theo base64.
  2. `strrev(...)` → đảo ngược chuỗi base64.
  3. `bin2hex(...)` → chuyển chuỗi thành dạng hex.

---

## 🔑 Cách bypass

- Ta sẽ dùng 1 đoạn code Python để **giải mã**:

```python
import base64

encode = "3d3d516343746d4d6d6c315669563362"
step1 = bytes.fromhex(encode).decode()
step2 = step1[::-1]
secret = base64.b64decode(step2).decode()
print(secret)
```

- Khi chạy đoạn code trên, ta sẽ nhận được **secret**.
- Quay lại màn hình nhập secret, nhập vào giá trị vừa giải mã được → màn hình sẽ hiện ra password cho level tiếp theo.

**✅ Password: `ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t`**
