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

# Task 2: CSRF Countermeasure implementation

## 2.1: Solution 1:

## 2.2: Solution 2: