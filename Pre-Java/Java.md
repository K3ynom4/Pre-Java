# CÁCH JAVA LƯU TRỮ DỮ LIỆU
Java lưu trữ dữ liệu theo hai loại chính: kiểu dữ liệu nguyên thuỷ (primitive) và kiểu dữ liệu tham chiếu (reference).
## 1.1 Kiểu dữ liệu nguyên thủy
- Kiểu dữ liệu nguyên thuỷ là các kiểu dữ liệu cơ bản của Java, bao gồm:
  - Kiểu số nguyên: byte, short, int, long
  - Kiểu số thực: float, double
  - Kiểu logic: boolean
  - Kiểu ký tự: char
> Ví dụ:
```Java
int x=10;
//dữ liệu x được lưu trữ trực tiếp trong bộ nhớ máy tính
//địa chỉ của x là:0x000000000400000
```
## 1.2 Kiểu dữ liệu tham chiếu
- Kiểu dữ liệu tham chiếu là các kiểu dữ liệu được sử dụng để tham chiếu đến một đối tượng. Các kiểu dữ liệu tham chiếu bao gồm:
  - Kiểu đối tượng: class, interface
  - Kiểu wrapper 
- Dữ liệu kiểu tham chiếu không được lưu trữ trực tiếp trong bộ nhớ máy tính, mà được lưu trữ dưới dạng một tham chiếu đến một đối tượng trong bộ nhớ heap. Tham chiếu này bao gồm địa chỉ của đối tượng trong bộ nhớ heap.
> ví dụ:
```Java
String s = "Hello, world!";
// Dữ liệu s không được lưu trữ trực tiếp trong bộ nhớ máy tính
// Địa chỉ của s là: 0x0000000000400000
// Dữ liệu "Hello, world!" được lưu trữ trong bộ nhớ heap
// Địa chỉ của "Hello, world!" là: 0x0000000000400100

```
### 1.2.1 Class object
- Class object là một đối tượng đại diện cho một lớp. Class object được lưu trữ trong bộ nhớ heap. Mỗi lớp chỉ có một class object duy nhất.
### 1.2.2 Wrapper
- Wrapper là các lớp được sử dụng để bao bọc các kiểu dữ liệu nguyên thuỷ. Mỗi kiểu dữ liệu nguyên thuỷ có một lớp wrapper tương ứng.
> Ví dụ:
  - Lớp *Integer* là wrapper của kiểu dữ liệu nguyên thuỷ *int*
  - Lớp *Double* là wrapper của kiểu dữ liệu nguyên thuỷ *double*
- Boxing
  - Boxing là quá trình chuyển đổi một giá trị kiểu dữ liệu nguyên thuỷ thành một đối tượng kiểu wrapper. Boxing được thực hiện bằng cách sử dụng phương thức *valueOf()* của lớp wrapper tương ứng.
> Ví dụ:
```Java
int x = 10;
Integer y = Integer.valueOf(x);

// y là một đối tượng kiểu Integer có giá trị là 10
```
- Unboxing
  - Unboxing là quá trình chuyển đổi một đối tượng kiểu wrapper thành một giá trị kiểu dữ liệu nguyên thuỷ. Unboxing được thực hiện bằng cách sử dụng phương thức *intValue()* của lớp wrapper tương ứng.
> Ví dụ:
```Java
Integer y = Integer.valueOf(10);
int x = y.intValue();

// x là một giá trị kiểu int có giá trị là 10

```
### 1.3 Từ khóa super
- Từ khóa super trong java là một biến tham chiếu được sử dụng để tham chiếu trực tiếp đến đối tượng của lớp cha gần nhất. Bất cứ khi nào bạn tạo ra instance (thể hiện) của lớp con, một instance của lớp cha được tạo ra ngầm định, nghĩa là được tham chiếu bởi biến super.Từ khóa super có 3 cách sử dụng sau:
  - Gọi trực tiếp hàm dựng **(constructor)**của lớp cha gần nhất.
  - Gọi trực tiếp thuộc tính **(field)**của lớp cha gần nhất.
  - Gọi trực tiếp phương thức **(method)**của lớp cha gần nhất.
> Ví dụ 1: Gọi trực tiếp constructor của lớp cha gần nhất

