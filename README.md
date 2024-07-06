# 20110494: Nguyễn Đình Quang Huy
# Task 1: normal transaction with CRSF vulnerability

## 1.1: Login, Check balance

Login vào trang chính của web với domain: http://127.0.0.1:5000/login

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/7c8fa777-598a-4a73-a412-184e0465ecf8)

Login với tài khoản: alice và mật khẩu là: alice

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/78beeae2-eace-46cb-be19-cca36b21cb05)

Vào kiểm tra balance và hiện ra dòng chữ 'Your balance is $10000' :

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/134377b7-7ec8-4bf1-882b-f7b5fc81be30)

## 1.2: Doing the transaction

Tiến hành giao dịch tới người tên là Bob với số tiền là 500:

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/268ff0b4-aee7-4fe0-a340-bb5fe966330e)

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/461345d5-51b2-49e3-b8ca-f6b36e2699ee)

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/5e46a472-1d48-4435-9ee6-17984b92770b)

Kiểm tra lại số dư của alice:

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/e61f90c0-e2a8-4233-a0e5-448289cf471d)

## 1.3: Tranfer money illegitimately

Ở file hidden_form.html thì trong phần action của form sửa lại đường dẫn sao cho giống với đường dẫn của file target.py và sau đó run file sẽ xuất hiện dòng chữ 'Transferred $1000 to account attacker':

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/b595ca2f-03fb-41d4-9fd8-442282e31a4b)

Qua tài khoản của alice và kiểm tra lại số dư thì đã bị mất đi 1000$:

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/b1065285-f449-4986-b58c-b92e660e14c9)

# Task 2: CSRF Countermeasure Implementation

## 2.1: Solution 1 - Mẫu đồng bộ hóa token

### 2.1.1. Tổng quan

Mẫu đồng bộ hóa token là một kỹ thuật bảo mật được sử dụng để ngăn chặn các cuộc tấn công CSRF (Cross-Site Request Forgery). Trong giải pháp này, một token duy nhất được tạo ra cho mỗi phiên người dùng và được gửi cùng với mỗi yêu cầu của người dùng. Token này sau đó được kiểm tra trên phía máy chủ để xác nhận tính hợp lệ của yêu cầu.

### Tạo CSRF token khi đăng nhập

Khi người dùng đăng nhập thành công, một CSRF token được tạo ra và lưu trữ trong một cookie phiên người dùng.

### Gắn token vào các yêu cầu POST

Token CSRF phải được bao gồm trong các form hoặc yêu cầu POST. Thường thì token này được ẩn dưới dạng input trong form.

### Xác thực token trên máy chủ

Khi một yêu cầu POST được gửi tới máy chủ, token CSRF từ yêu cầu được so sánh với token được lưu trong phiên người dùng. Nếu token hợp lệ, yêu cầu được xử lý; nếu không, yêu cầu bị từ chối.


Đây là demo:

Login và làm mọi thứ như bình thường:

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/777cc283-a8ac-446b-a05d-7c98abcc8f19)

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/ff718d63-3a49-4061-acac-ed52b2ee5246)

Sau khi login xong thì tạo ra 1 token và lưu bên trong cookies và bây giờ muốn gửi form thì phải có token thì mới thực hiện được:

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/abef6823-0c59-4e6c-8c7b-ff12620a1e06)

Tiến hành kiểm tra số dư và chuyển tiền như bình thường:

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/2e9ea5fa-efe7-4f6d-887c-01c06de42149)


![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/bda33c14-c9be-402c-a036-390c850334d5)


![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/82aa847c-0106-4094-bfee-cb32a8efdbc3)

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/7c5f7dfd-3636-44b1-ad74-3794aa995c0c)

Sau đó mở file html để tiến hành đánh cắp số tiền:

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/dcaee699-175d-4fbb-a253-c84797396e25)

Lúc này không có token thì form html sẽ không đánh cắp số tiền được và tiến hành kiểm tra số dư

![image](https://github.com/MiloHuy/CSRF_Attack_Lab_20110494/assets/91107200/2a3aa2f8-95cb-477d-81d4-ccdfd41e2b0c)

Vậy là đã bảo vệ thành công.
