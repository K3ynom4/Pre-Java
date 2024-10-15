# [JAVA BUỔI 7] INTERFACE VÀ TRỪU TƯỢNG

## 1.INTERFACE
- **Interface** là một bản thiết kế của một lớp. Nó chỉ có các phương thức trừu tượng. 
- **Interface** là một kỹ thuật để thu được tính trừu tượng hoàn toàn và đa kế thừa trong Java. Một interface trong Java cũng biễu diễn mối quan hệ "IS-A"
- Một interface không phải là **một lớp**. Viết một interface giống như viết một lớp, nhưng chúng có 2 định nghĩa khác nhau. Một **lớp** mô tả các thuộc tính và hành vi của một đối tượng. Một **interface** chứa các hành vi mà một class triển khai.
- Một interface trong Java là một tập hợp các phương thức trừu tượng (abstract). Một class triển khai một interface, do đó kế thừa các phương thức abstract của interface.
## 2.INTERFACE VÀ ABSTRACT CLASS
- **Lớp trừu tượng** (Abstract Class):
  - Là một lớp nhưng không thể tạo ra thực thể. Abstract class có thể chứa hoặc không chứa phương thức abstract – một phương thức chỉ có khai báo mà không chứa cài đặt.
  ```Java
    abstract class Cars
    {
        int gas;
        int getGas()
        {
            return this.gas;
        }

        abstract void run();
    }

    class Merc extends Cars
    {
        void run()
        {
                print("Fast");
        }
    }
  
  ```
    > **Giải thích**: khai báo một lớp trừu tượng Cars. Các phương thức của lớp trừu tượng Cars sẽ được kế thừa bởi các lớp con.
- **Interface**
  - Một interface không phải là một lớp (class), giống như lớp trừu tượng. Nó chứa các phương thức mà không phần thân. Một interface không thể tự làm bất cứ điều gì. Interface như một khuôn mẫu. Với ngôn ngữ Java không hỗ trợ đa kế thừa nhưng có thể triển khai nhiều interface.
  ```Java
    interface Cars
    {
        void run();
        int getGas();
    }
    class Merc implements Cars
    {
        int gas;
        void run()
        {
            print("Faster");
        }
        int getGas()
        {
            return this.gas;
        }
    }
  ```
  >**Giải thích**: các phương thức của interface không có phần thân, chỉ xác định kiểu dữ liệu trả về và tên phương thức, không giống như lớp trừu tượng đã khai báo trước đó.
### 2.1 Sự khác biệt giữa Abtract class và Interface
- Một interface chứa một tập hợp các phương thức. Một lớp implements interface phải triển khai các phương thức này.

- Một lớp trừu tượng, giống như một interface, sẽ chứa các phương thức. Tuy nhiên, sẽ có ít nhất một phương thức đã hoàn thành tức là phương thức có phần thân.
 ![Alt text](image-17.png)
### 2.2 Sự giống nhau giữa interface và abstract class
- Không thể tạo một biến kiểu interface hoặc abstract class.
- Nếu là phương thức abstract thì phải được khai báo lại trong class con.
- Cả interface và abstract class đều có tính kế thừa.
### 2.3 Khi nào thì sử dụng interface và abstract class
- Khi một nhóm đối tượng có cùng bản chất kế thừa từ một class thì sử dụng abstract class.

- Khi một nhóm đối tượng không có cùng bản chất nhưng chúng có hành động giống nhau thì sử dụng interface.
## 3.TÍNH TRỪU TƯỢNG
### 3.1 Khái niệm
- Tính trừu tượng trong Java là tính chất không thể hiện cụ thể mà chỉ nêu tên vấn đề. Đó là một quá trình che giấu các hoạt động bên trong và chỉ hiển thị những tính năng thiết yếu của đối tượng tới người dùng.
    >Ví dụ: một người sử dụng điện thoại để gửi tin nhắn thì anh ta sẽ nhập nội dung tin nhắn, thông tin người nhận và ấn nút gửi. Khi anh ta bắt đầu gửi tin thì anh ấy không biết những gì diễn ra bên trong quá trình gửi mà chỉ biết được là kết quả của tin nhắn đã được gửi đến người nhận thành công hay chưa.
    Vì vậy trong ví dụ này, quá trình gửi tin nhắn đã được ẩn đi và chỉ hiển thị những chức năng mà người dùng cần đó là chức năng nhập nội dung tin nhắn, thông tin người nhận, kết quả gửi tin nhắn thành công hay thất bại. Đó chính là tính trừu tượng.
### 3.2 Phương thức trừu tượng ( Abstract class)
- Các phương thức chỉ có phần khai báo mà không có thân phương thức nằm trong cặp dấu {} và có một dấu chấm phẩy để kết thúc được gọi là phương thức trừu tượng. Để định nghĩa một phương thức là phương thức trừu tượng chúng ta sẽ sử dụng từ khóa abstract đứng trước tên phương thức.
-  Cú pháp: 
    > [access_modifier] abstract [kiểu_trả_về][tên_phương_thức_trừu_tượng][<đối_số_truyền_vào>];
        
- Trong đó:

    **[access_modifier]** là phạm vi truy cập của phương thức trừu tượng. Phạm vi truy cập của phương thức trừu tượng tương tự như của các phương thức bình thường nhưng không được khai báo phạm vi truy cập là **private**, nếu để là **private** thì trình biên dịch sẽ báo lỗi.
    **[kiểu_trả_về]** là kiểu dữ liệu của phương thức.
    **[tên_phương_thức_trừu_tượng]** phải tuân theo quy tắc đặt tên phương thức (hàm) của Java.
    Phương thức này có thể có hoặc không có **<đối_số_truyền_vào>**.
    **Ví dụ:**
    ```Java
    public abstract khaiBaoPhuongThucTruuTuong();
    ```
    **Lưu ý**: Để sử dụng phương thức trừu tượng này, chúng ta cần phải ghi đè (override) nó trong lớp con kế thừa trực tiếp lớp khai báo phương thức này.
### 3.3 Lớp trừu tượng
- Lớp trừu tượng là lớp được khai báo với từ khóa abstract đứng trước tên của lớp.
- Nếu 1 lớp được khai báo là 1 lớp trừu tượng thì chúng ta không thể dùng trực tiếp nó để tạo ra đối tượng mà phải viết một lớp kế thừa của lớp trừu tượng đó.
- Lớp trừu tượng có thể có hoặc không có phương thức trừu tượng. Nếu một lớp có ít nhất 1 phương thức trừu tượng thì lớp đó phải được khai báo là lớp trừu tượng.
- Những lớp là lớp trừu tượng cũng không cần có phương thức khởi tạo.
- Một khi có một lớp nào đó kế thừa lớp trừu tượng thì lớp con đó bắt buộc phải override lại nội dung tất cả các phương thức trừu tượng có trong lớp đó.
>**Tóm lại, lớp trừu tượng là 1 lớp không thể khởi tạo đối tượng từ nó, nhưng nó lại ràng buộc các lớp con kế thừa trực tiếp nó phải có các phương thức trừu tượng của nó thông qua sự ghi đè (override) phương thức.**
