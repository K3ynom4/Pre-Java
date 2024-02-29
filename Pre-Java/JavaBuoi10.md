# [JAVA] - BUỔI 10: NHẬP XUẤT FILE, UNIT TEST

Tầm quan trọng của việc viết Unit test
## 1. Xử lí File trong Java (Binary file, Text file):

- Xử lí file trong Java:
    - Đọc và ghi file trong java là các hoạt động nhập/xuất dữ liệu (nhập dữ liệu từ bàn phím, đọc dữ liệu từ file, ghi dữ liệu lên màn hình, ghi ra file, ghi ra đĩa, ghi ra máy in…) đều được gọi là luồng (stream).
    - Có 2 kiểu luồng (stream) trong Java:
        - Byte Stream: Hỗ trợ nhập xuất dữ liệu trên byte -> Binary file
          - Dữ liệu dạng nhị phân
          - 2 abstract class: InputStream (đọc) và OutputStream (ghi)
        - Character Stream: Hỗ trợ nhập xuất kiểu kí tự -> Text file
          - Dự liệu dạng kí tự Unicode
          - 2 abstract class: Reader và Writer

- Đọc ghi 1 file:
    - Bước 1: Tạo đối tượng luồng và liên kết với nguồn dữ liệu.
    - Bước 2: Thao tác dữ liệu (đọc hoặc ghi hoặc cả hai).
    - Bước 3: Đóng luồng.
- Tạo file
```Java
    import java.io.File;  // Import the File class
    import java.io.IOException;  // Import the IOException class to handle errors

    public class CreateFile {
        public static void main(String[] args) {
            try {
            File myObj = new File("filename.txt");
            if (myObj.createNewFile()) {
                System.out.println("File created: " + myObj.getName());
            } else {
                System.out.println("File already exists.");
            }
            } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
            }
        }
    }
    // output: File created: filename.txt
```
- Ghi file :
    ```Java
    import java.io.FileWriter;   // Import the FileWriter class
    import java.io.IOException;  // Import the IOException class to handle errors

    public class WriteToFile {
        public static void main(String[] args) {
            try {
            FileWriter myWriter = new FileWriter("filename.txt");
            myWriter.write("Files in Java might be tricky, but it is fun enough!");
            myWriter.close();
            System.out.println("Successfully wrote to the file.");
            } catch (IOException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
            }
        }
    }
    ```
- Đọc file:
``` java
    import java.io.File;  // Import the File class
    import java.io.FileNotFoundException;  // Import this class to handle errors
    import java.util.Scanner; // Import the Scanner class to read text files

    public class ReadFile {
        public static void main(String[] args) {
            try {
            File myObj = new File("filename.txt");
            Scanner myReader = new Scanner(myObj);
            while (myReader.hasNextLine()) {
                String data = myReader.nextLine();
                System.out.println(data);
            }
            myReader.close();
            } catch (FileNotFoundException e) {
            System.out.println("An error occurred.");
            e.printStackTrace();
            }
        }
    }
```
- Lấy thông tin của 1 file:
```Java
    import java.io.File;  // Import the File class

    public class GetFileInfo { 
        public static void main(String[] args) {
            File myObj = new File("filename.txt");
            if (myObj.exists()) {
            System.out.println("File name: " + myObj.getName());
            System.out.println("Absolute path: " + myObj.getAbsolutePath());
            System.out.println("Writeable: " + myObj.canWrite());
            System.out.println("Readable " + myObj.canRead());
            System.out.println("File size in bytes " + myObj.length());
            } else {
            System.out.println("The file does not exist.");
            }
        }
    }
    /*
    File name: filename.txt
    Absolute path: C:\Users\MyName\filename.txt
    Writeable: true
    Readable: true
    File size in bytes: 0
    */
```
- Xóa 1 file:
```java
    import java.io.File;  // Import the File class

    public class DeleteFile {
        public static void main(String[] args) { 
            File myObj = new File("filename.txt"); 
            if (myObj.delete()) { 
            System.out.println("Deleted the file: " + myObj.getName());
            } else {
            System.out.println("Failed to delete the file.");
            } 
        } 
    }
```
### 1.1 Text file
- Text file là một loại file chứa dữ liệu được biểu diễn dưới dạng văn bản.
- Dữ liệu trong text file được lưu trữ dưới dạng các ký tự, sử dụng một bộ mã như ASCII hoặc Unicode.
- Text file có thể chứa nội dung như văn bản, mã nguồn, dữ liệu được lưu trữ dưới dạng chuỗi các ký tự. 
- Ví dụ:
    Đọc/ghi dữ liệu từ/ra text file:
    ```java 
        import java.io.BufferedReader;
        import java.io.BufferedWriter;
        import java.io.FileReader;
        import java.io.FileWriter;
        import java.io.IOException;

        public class TextFileExample {
            public static void main(String[] args) {
                String filePath = "path/to/textfile.txt";
                
                try (BufferedReader reader = new BufferedReader(new FileReader(filePath));
                    BufferedWriter writer = new BufferedWriter(new FileWriter(filePath))) {
                    
                    // Đọc dữ liệu từ text file
                    String line;
                    while ((line = reader.readLine()) != null) {
                        System.out.println(line);
                    }
                    
                    // Ghi dữ liệu vào text file
                    writer.write("Hello, world!");
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }
        }
    ```
### 1.2 Binary file
- Binary file là một loại file chứa dữ liệu được biểu diễn dưới dạng nhị phân (binary).
- Dữ liệu trong binary file được lưu trữ dưới dạng các byte, không được biểu diễn trực tiếp như văn bản.
- Binary file có thể chứa nội dung như hình ảnh, âm thanh, video, các định dạng tệp tin nhị phân khác.
- ví dụ:
```Java
    import java.io.FileInputStream;
    import java.io.FileOutputStream;
    import java.io.IOException;

    public class BinaryFileExample {
        public static void main(String[] args) {
            String filePath = "path/to/binaryfile.bin";
            
            try (FileInputStream fis = new FileInputStream(filePath);
                FileOutputStream fos = new FileOutputStream(filePath)) {
                
                // Đọc dữ liệu từ binary file
                byte[] buffer = new byte[1024];
                int bytesRead;
                while ((bytesRead = fis.read(buffer)) != -1) {
                    // Xử lý dữ liệu
                }
                
                // Ghi dữ liệu vào binary file
                byte[] data = {0x01, 0x02, 0x03};
                fos.write(data);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
```
## 2. Assertions
- Assertions trong Java là một tính năng mạnh mẽ để kiểm tra các giả định trong chương trình. Chúng giúp đảm bảo rằng các điều kiện cần thiết được thỏa mãn trong quá trình thực thi và giúp phát hiện lỗi và sự không nhất quán trong mã nguồn.

- Cú pháp của một lệnh assertion trong Java như sau:
```Java
    assert expression;
```
- Khi một lệnh assertion được thực thi, biểu thức trong assert sẽ được đánh giá. Nếu giá trị của biểu thức là true, không có hành động gì xảy ra và chương trình tiếp tục thực thi. Ngược lại, nếu giá trị của biểu thức là false, một AssertionError sẽ được ném ra và chương trình sẽ dừng lại.

- Một lệnh assertion có thể có một thông điệp để cung cấp thông tin bổ sung về lỗi. Cú pháp của một lệnh assertion với thông điệp như sau:
```java
    assert expression : message;// message là một biểu thức kiểu chuỗi (String) chứa thông điệp.
```
- Mặc định, assertions bị vô hiệu hóa. Chúng ta cần chạy mã như sau để kích hoạt lệnh:
    **Để kích hoạt:** java –ea Test hoặc java –enableassertions Test
    **Để vô hiệu hóa:** java –da Test hoặc java –disableassertions Test
- Ở đây, Test là tên file.
- Tuy nhiên, cần lưu ý rằng assertions không nên được sử dụng để thay thế cho việc xử lý lỗi hoặc để kiểm tra các đối số trong các phương thức công khai vì chúng có thể được cung cấp bởi người dùng.
- ví dụ
```java
import java.util.Scanner;
 
class Test {
    public static void main(String args[])
    {
        int value = 15;
        assert value >= 20 : " Underweight";
        System.out.println("value is " + value);
    }
}
```
## 3. Unit Test
- Unit testing là một phương pháp kiểm thử phần mềm mà trong đó các phần riêng lẻ của mã nguồn (đơn vị) được kiểm tra độc lập để xác định xem chúng hoạt động đúng hay không. Mục tiêu của unit testing là đảm bảo chất lượng của các đơn vị mã nguồn và tăng tính tin cậy của hệ thống.
- ví dụ: 
```java
    import org.junit.jupiter.api.Assertions;
    import org.junit.jupiter.api.Test;

    public class CalculatorTest {

        @Test
        public void testAddition() {
            Calculator calculator = new Calculator();
            int result = calculator.add(2, 3);
            Assertions.assertEquals(5, result);
        }

        @Test
        public void testDivision() {
            Calculator calculator = new Calculator();
            double result = calculator.divide(10, 2);
            Assertions.assertEquals(5.0, result, 0.0001);
        }
    }
    - Trong ví dụ trên, chúng ta tạo ra một lớp Calculator để thực hiện các phép tính đơn giản như cộng và chia. Tiếp theo, chúng ta tạo một lớp CalculatorTest để viết các unit tests cho lớp Calculator. Hai phương thức kiểm thử testAddition() và testDivision() được chú thích bằng @Test để đánh dấu chúng là các phương thức kiểm thử. Trong các phương thức kiểm thử này, chúng ta sử dụng các phương thức từ lớp Assertions của JUnit để kiểm tra kết quả của các phép tính.
```
- Tầm quan trọng của unit test
- Đảm bảo chất lượng: Unit testing giúp đảm bảo chất lượng của mã nguồn bằng cách kiểm tra từng đơn vị mã nguồn độc lập. Nó cho phép kiểm tra tính chính xác và đáng tin cậy của các phần riêng lẻ trong môi trường kiểm thử điều kiện kiểm soát.

- Phát hiện lỗi sớm: Unit testing giúp phát hiện lỗi sớm trong quá trình phát triển. Bằng cách kiểm tra từng đơn vị mã nguồn, các lỗi có thể được phát hiện ngay khi chúng xảy ra, giúp giảm thiểu sự lan truyền và ảnh hưởng tiêu cực đến toàn bộ hệ thống.

- Hỗ trợ sửa lỗi: Khi một lỗi được phát hiện trong quá trình unit testing, nó giúp xác định nguyên nhân gốc rễ của lỗi và thu hẹp phạm vi sửa lỗi. Điều này giúp việc sửa lỗi trở nên dễ dàng hơn và hạn chế ảnh hưởng đến các phần khác của hệ thống.

- Tăng tính ổn định và độ tin cậy: Unit testing giúp tăng tính ổn định và độ tin cậy của hệ thống. Khi các đơn vị mã nguồn đã được kiểm tra và xác minh, khả năng hệ thống hoạt động đúng và ổn định tăng lên, giảm thiểu rủi ro lỗi và sự không nhất quán.

- Hỗ trợ tái cấu trúc và bảo trì: Việc viết unit tests yêu cầu tách biệt các phần mã nguồn và thiết kế chúng sao cho có tính tái sử dụng cao. Điều này giúp cải thiện cấu trúc mã nguồn và dễ dàng bảo trì mã nguồn sau này.

- Tăng sự tự tin và giảm rủi ro: Unit testing giúp tăng sự tự tin của nhà phát triển và nhóm phát triển trong việc thực hiện các thay đổi và tối ưu hóa mã nguồn. Nó giúp giảm rủi ro gây ra các lỗi không mong muốn và tăng tính ổn định của hệ thống.

- Hỗ trợ quy trình phát triển: Unit testing được tích hợp vào quy trình phát triển phần mềm như phát triển dựa trên kiểm thử (test-driven development) hoặc kiểm thử liên tục (continuous testing). Nó đóng vai trò quan trọng trong việc đảm bảo chất lượng và sự ổn định của mã nguồn trong suốt quy trình phát triển.
