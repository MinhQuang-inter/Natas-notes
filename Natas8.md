# prokyurem

Natas level 8.

## Nội dung đầu bài

- Khi đăng nhập vào natas8 bạn sẽ chỉ thấy có ô '''input secret'''
  -> Màn này muốn chúng ta tìm ra secret để điền vào ô đó khi đó ta sẽ tìm được password cho màn tiếp theo
- Ta nhìn bên cạnh thì sẽ thấy được dòng view '''sourcecode'''
- Khi ta ấn vào ta sẽ thấy một đoạn code PHP đó chính là gợi ý cho ta làm
  '''$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($\_POST['secret']) == $encodedSecret) {
print "Access granted. The password for natas9 is <censored>";
} else {
print "Wrong secret";
}
} '''

- Nó thực hiện 3 bước
  1.base64_encode($secret) -> mã hóa chuỗi theo base64.
  2.strrev(...) -> đảo ngược chuỗi base64.
  3.bin2hex -> chuyển chuỗi thành dạng hex

### Cách bypass

- Ta sẽ dùng 1 đoạn code python để giải mã
  ''' import base64
  encode = "3d3d516343746d4d6d6c315669563362"
  step1 = bytes.fromhex(encode).decode()
  step2 = step1[::-1]
  secret = base64.b64decode(step2).decode()
  print(secret)

  -> Khi chạy đoạn code ta sẽ nhận được secret, quay lại màn trang chủ nhập đoạn mã secret ta vừa nhận được màn hình sẽ hiện ra password cho màn tiếp theo
  ** Password : ZE1ck82lmdGIoErlhQgWND6j2Wzz6b6t **
