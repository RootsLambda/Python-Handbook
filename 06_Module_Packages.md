# 6.1 Tại sao phải sử dụng module?
Các module cung cấp cho chúng ta có thể dễ dàng tổ chức các thành phần 
trong một hệ thống bằng cách dưới dạng các gói packages chứa các biến được gọi là không gian tên namespaces. 
Module có hai vai trò phổ biến:

+ **Sử dụng lại mã**

  Các module cho phép bạn lưu mã trong tệp vĩnh viễn, mã trong các tệp module là liên tục và nó có thể được tải lại và 
  chạy lại bao nhiêu khi cần thiết.
+ **Phân vùng không gian tên hệ thống**

  Module cũng là đơn vị tổ chức chương trình cấp cao nhất trong Python. 
  Mặc dù về cơ bản chúng chỉ là các gói tên các gói này cũng độc lập, bạn không bao giờ có thể thấy tên trong một tệp khác, 
  trừ khi bạn nhập rõ ràng tên đó tập tin. 
  Giống như các phạm vi cục bộ trong hàm số giúp ta tránh xung đột tên giữa các chương trình của bạn. 
  
## Cấu trúc của một chương trình Python
Ở cấp cơ sở, một chương trình Python bao gồm các tệp văn bản chứa các câu lệnh Python,
với một tệp chính top-level hoặc nhiều tệp bổ sung được gọi là module.

+ Tệp top-level chứa luồng điều khiển chính của chương trình của bạn, đây là tệp bạn chạy để khởi chạy ứng dụng của mình. 

+ Các tệp module là thư viện các công cụ được sử dụng để thu thập các thành phần được sử dụng bởi tệp top-level và có thể
ở nơi khác. 

Hình bên dưới mô tả cấu trúc của chương trình Python bao gồm ba tệp: a.py, b.py và c.py. 
Tệp a.py được chọn làm tập top-level, nó sẽ là một tệp văn bản đơn giản của các câu lệnh, 
được thực thi từ trên xuống dưới cùng khi khởi chạy. 
Các tệp b.py và c.py là các module chúng cũng là những tập tin văn bản đơn giản
cũng như các câu lệnh, nhưng chúng thường không được đưa ra trực tiếp.

<img align='center' src='images/Module_a.jpg'>

Ví dụ: Tệp b.py có hàm số là spam
```python
def spam(text): # File b.py
    print(text,'spam')
```
Nội dụng tệp top-level
```python
import b
b.spam('gumby')
```
`Output: gumby spam`

Module thư viện tiêu chuẩn là một số module mà chương trình của bạn
sẽ khi tạo được cung cấp bởi chính Python và không phải là các tệp bạn sẽ viết mã.
Bộ sưu tập này có hơn 200 module lớn chứa hỗ trợ độc lập với nền tảng cho các tác vụ lập trình thông thường.
## Các import hoạt động
Chúng là các hoạt động thời gian chạy khi một chương trình nhập một tệp lần đầu tiên được chạy sẽ thực hiện 3 bước:

1. Tìm tệp của module.
2. Biên dịch nó thành mã byte (nếu cần).
3. Chạy mã của module để xây dựng các đối tượng mà nó xác định.
## Không gian tên module
Module có lẽ được hiểu đơn giản là các gói tên. Về mặt kỹ thuật, các module
thường tương ứng với các tệp và Python tạo một đối tượng module để chứa tất cả các tên
được chỉ định trong một tệp module. Nhưng thật chất, module chỉ là không gian tên (địa điểm
nơi các tên được tạo) và các tên tồn tại trong một module được gọi là các thuộc tính của nó.

Không gian tên module có thể được truy cập thông qua thuộc tính__dict__ hoặc dir(M).

```python
print('starting to load...') # File module1.py
name = 42
def func(): pass
class klass: pass

print('done loading.')
```
Kiểm tra thuộc tính của module thông qua \_\_dict\_\_
```python
import module1
list(module1.__dict__.keys())
```
`Output: ['__name__', '__doc__', '__package__', '__loader__', '__spec__', '__file__', '__cached__', '__builtins__', 'name', 'func', 'klass']`
## Reloading Module
Các của module chỉ được chạy một lần cho chạy chương trình. Để có thể gọi lại module để chạy lại ta có thể gọi hàm **reload**
trong built-in function.
```python
X=5 # File changer.py
```
Ta thực hiện reload sau đây
```python
import changer

changer.X = 10
print(chager.X)

import changer
print(changer.X)

from importlib import reload

reload(changer)
print(changer.X)
```
Ouput:
```
10
10
5
```
# 6.2 Module Packages với \_\_init\_\_.py file
Đây là một tính năng nâng cao, nhưng hệ thống phân cấp cung cấp cho chúng ta rất tiện dụng
để tổ chức các tệp trong một hệ thống lớn và làm đơn giản hóa đường dẫn tìm kiếm module cài đặt.

Khi bạn ở thư mục đang làm việc bạn có thể import thư mục .py bằng

import dir1.dir2.mod

from dir1.dir2.mod import x

Đường dẫn có dấu "chấm" sẽ giả định là tương ứng với một đường dẫn qua
phân cấp thư mục trên máy tính của bạn, dẫn đến tệp mod.py, như trong thư mục ở Windows sẽ được hiểu là:

dir0/dir1/dir2/mod.py

nếu bạn muốn sử dụng với import packages, có một ràng buộc nữa bạn phải tuân theo là mỗi thư mục có tên trong đường dẫn packages phải chứa tệp có tên \_\_init\_\_.py, theo quy tắc này ta có:
+ dir1 và dir2 cả hai phải có file \_\_init\_\_.py
+ dir0 là container không yêu cầu phải chứa file \_\_init\_\_.py
+ dir0 bắt buộc là danh sách trên module trên tìm kiếm đường dẫn sys.path
```
dir0\                         # Container on module search path
  dir1\
    __init__.py
      dir2\
        __init__.py
        mod.py
```
Các tệp \_\_init\_\_.py có thể chứa mã Python hoặc không chứa gì và giống như các tệp module bình thường. Nhưng tên của chúng
đặc biệt vì mã của chúng được chạy tự động vào lần đầu tiên một chương trình Python, đóng vai trò như một mắt xích để thực hiện các bước khởi tạo theo yêu cầu của packages. 

# 6.3 Sử dụng \_\_name\_\_ và \_\_main\_\_
Mỗi module có một thuộc tính trong built-in được gọi là \_\_name\_\_, thuộc tính này
Python tạo và gán tự động như sau:
+ Nếu tệp đang được chạy dưới dạng tệp chương trình top-level, \_\_name\_\_ được đặt thành 
"\_\_main\_\_".
+ Nếu tệp đang được import khi đó \_\_name\_\_ được đặt thành tên của module.

Điều này giúp chúng ta có thể kiểm tram module \_\_name\_\_ xác định xem nó có đang
run hoặc import. Xem ví dụ sau
```python
def tester():                           # File runme.py
    print("It's Christmas in Heaven...")
    print(__name__)
if __name__ == '__main__': # Only when run
    tester()               # Not when imported
```
Output:
```
It's Christmas in Heaven...
__main__
```
Khi import từ khách hàng
```python
import runme
runme.tester()
```
Output:
```
It's Christmas in Heaven...
runme
```

