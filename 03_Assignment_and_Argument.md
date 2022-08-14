# 3.1 Giới thiệu Assignment Statements
Chúng ta sử dụng phép gán bằng cách gán object bên phải cho name bên trái một số điều cần lưu ý là: 

+ **Phép gán tạo tham chiếu đối tượng:** các phép gán trong Python lưu trữ các tham chiếu đến các đối tượng trong tên hoặc các thành phần cấu trúc dữ liệu, chúng luôn tạo tham chiếu đến các đối tượng thay vì sao chép các đối tượng. Vì lý do đó, các biến Python giống như con trỏ hơn là vùng lưu trữ dữ liệu.
+ **Tên được tạo khi được gán lần đầu:** Python tạo một tên biến đầu tiên thời gian bạn gán cho nó một giá trị(tức là một tham chiếu đối tượng), vì vậy không cần khai báo trước như một vài ngôn ngữ khác. 
+ **Tên phải được chỉ định trước khi được tham chiếu:** Sẽ xảy lỗi khi sử dụng cái tên nào đó mà bạn chưa chỉ định giá trị. Python đưa ra một ngoại lệ. Điều này hóa ra là rất quan trọng trong Python vì tên không được khai báo trước.

+ **Một số hoạt động thực hiện phép gán ngầm.**
## Các assignment thường dùng
| Phép tính   | Giải thích | 
| :---        |    :----   |   
| a='spam'     | basic form      | 
| a,b='spam','yumy   | tuple assignment       | 
|[a,b]=['spam','yumy']|list assignment|
|a,b,c,d='spam'|sequence assignment|
|a,\*b='spam'|extended sequence unpacking|
|a=b='spam'|multiple assignment
|a+=2|augmented assignment(a=a+2)|
### Sequence Assignments
```python
[a,b,c]=(1,3,4) # Assign tuple values to list name
a
```
`Output: 1`
```python
(A,B,C)="spa" # Assign string values to tuple name
B
```
`Output: 'p'`
```python
a,b,c,d='spam'
c
```
`Output: 'a'`
```python
red, green,blue=range(3)
red
```
`Output: 0`
### Extended Sequence Unpacking
```python
*a,b='spam' # a sẽ nén phần còn lại của chuỗi khi assign
a
```
`Output: ['s', 'p', 'a']`
```python
a,*b,c='spam' 
b
```
`Output: ['p', 'a']`
```python
a,b,*c='spam'
c
```
`Output: ['a', 'm']`
```python
a,b,c,d,*e='spam'
e
```
`Output: []`

Khi nén 2 biến b và c sẽ xảy ra tình trạng lỗi. 

```python
a,*b,*c='spam'
```
`Output: SyntaxError: two starred expressions in assignment`

Khi bên name chỉ phải có 1 biến name không phải là nén.

```python
*a='spam'
```
`Output:SyntaxError: starred assignment target must be in a list or tuple`

Sửa lỗi như sau:
```python
*a,='spam'
a
```
`Output: ['s', 'p', 'a', 'm']`
### Unpacking với for loop
```python
for (a,*b,c) in [(1,2,3,4),(5,6,7,8)]:
    print(a,b,c,sep=',',end='\n')
 ```
 ```
 Output: 1,[2, 3],4
         5,[6, 7],8
  ```
  ```python
  for (i,j) in [(1,2),(3,2)]:
    print(i,j,sep=',')
  ```
 ```
 Output: 1,2
         3,2
 ```      
 # 3.2 Argument
Như chúng ta sẽ thấy, các đối số (còn gọi là tham số) được gán cho tên trong một hàm.
Python cung cấp các công cụ bổ sung, chẳng hạn như keywords, default và collectors đối số tùy ý và trình trích xuất cho phép linh hoạt trong cách các đối số được gửi đến một hàm.

## Tóm tắt các nhiệm vụ của đối số:

+ **Các đối số được chuyển bằng cách tự động gán các đối tượng cho biến cục bộ những cái tên.** Các đối số của hàm, tham chiếu đến các đối tượng được chia sẻ được gửi bởi người gọi. Vì tham khảo được triển khai dưới dạng con trỏ, tất cả các đối số, trên thực tế, được truyền bởi con trỏ. Các đối tượng được truyền dưới dạng các đối số không bao giờ được sao chép tự động.

+ **Việc gán cho các tên đối số bên trong một hàm không ảnh hưởng đến trình gọi.** Tên đối số trong defalts hàm trở thành tên cục bộ mới khi hàm chạy chỉ trong phạm vi của hàm đó.

+ **Thay đổi đối số đối tượng có thể thay đổi trong một hàm có thể ảnh hưởng đến lời gọi.** Mặt khác, vì các đối số chỉ được gán cho các đối tượng được truyền vào, các hàm có thể thay đổi các đối tượng có thể thay đổi được truyền vào tại chỗ và kết quả có thể ảnh hưởng đến lời gọi. Các đối số có thể thay đổi có thể là đầu vào và đầu ra cho các hàm.
## Cách truyền của Python:

+ **Các đối số bất biến(Immutable arguments) được truyền "theo giá trị".** Các đối tượng như số nguyên và chuỗi được chuyển bằng tham chiếu đối tượng thay vì bằng cách sao chép, và bạn cũng không thể thay đổi các đối tượng bất biến bằng một giá trị nào đó, trừ khi bạn tạo ra bản sao.
+ **Các đối số có thể thay đổi(Mutable arguments) được truyền "bằng con trỏ".** Các đối tượng như danh sách và từ điển cũng được chuyển bằng tham chiếu đối tượng.
### Share Reference
```python
def f(a): # a là phân phát đến tham khảo (references) của đối tượng
    a=99  # a chỉ là biến địa phương local
b=88
f(b)
print(b) # b không thay đổi 
```
`Output: 88`

**Đối với biến mutable**

```python
def changer(a, b): # Arguments assigned references to objects
    a = 2 
    b[0] = 'spam'
X = 1
L = [1, 2] # Caller:
changer(X, L) # Pass immutable and mutable objects
X, L
```
`Output: (1, ['spam', 2])`

**Tránh sự thay đổi của biến mutable**

```python
L = [1, 2]
changer(X, L[:])
X,L
```
`Output: (1, [1, 2])`
## Cú pháp cho argument
| Cú pháp   | Chức năng | Giải thích|
| :---        |    :--------     | :-----|  
| func(value)     | Lời gọi hàm  | Normal argument: truyền vào bởi vị trí|
| func(name=value)| Lời gọi hàm  | Keyword argument: truyền vào bởi tên|
| func(\*iterable)| Lời gọi hàm  | Chuyển tất cả các đối tượng iterable như các đối số vị trí riêng biệt|
| func(\*\*dict)| Lời gọi hàm    | Chuyển tất cả các cặp key/value trong dict như keyword argument riêng biệt|
| def func(name)| Hàm số     | Normal argument:truyền theo vị trí hoặc tên
| def func(name=value)| Hàm số   | Default argument value, lời gọi nó có thể có hoặc không|
| def func(\*name)| Hàm số     | Nhận các đối số positional còn lại của tuple|
| def func(\*\*name)| Hàm số  | Nhận có đối số keyword còn lại của dictionary|
| def func(\*other,name)| Hàm số    | Các đối số được truyền khi trong lời gọi|
| def func(\*,name=value)| Hàm số  | Các đối số được truyền khi trong lời gọi|

### Truyền bởi vị trí
```python
def f(a, b, c): 
    print(a, b, c)
f(1,2,3)
```
`Output: 1 2 3`

### Truyền bởi tên
```python
def f(a=1, b=2, c): 
    print(a, b, c)
f(3)
```
`Output: 1 2 3`

### Truyền bởi iterable
```python
def f(*args): 
    print(args)
f(3,4,4)
```
`Output: (3 4 4)
### Truyền bởi dictionary
```python
def f(**args): 
    print(args)
f(x=4,y=5)
```
`Output: {'x': 4, 'y': 5}`
### Truyền hỗn hợp normal, iterable, dictionary
```python
def f(a, *pargs, **kargs): 
    print(a, pargs, kargs)
f(1,2,3,x=4,y=5)
```
`Output: 1 (2, 3) {'x': 4, 'y': 5}`

### Lời gọi arguments
```python
def func(a, b, c, d): # hàm số định nghĩa kiểu normal
    print(a, b, c, d)
args=(1,2,3,4) # tuple
func(*args) # Nén thành argument
```
`Output: 1 2 3 4`
### Lời gọi keyword arguments
```python
kwargs = {'a': 1, 'b': 2, 'c': 3,'d':4}
func(**kwargs)
```
`Output: 1 2 3 4`
### Lời gọi hỗn hợp 
```python
func(1, *(2, 3), **{'d': 4})
```
`Output: 1 2 3 4`
```python
func(1, c=3, *(2,), **{'d': 4})
```
`Output: 1 2 3 4`
### Tạo ra hàm print trong Python 3
```python
# Call signature: print3(*args, sep=' ', end='\n', file=sys.stdout)
import sys
def print3(*args, **kargs):
    sep = kargs.get('sep', ' ') # Keyword arg defaults
    end = kargs.get('end', '\n')
    file = kargs.get('file', sys.stdout)
    output = ''
    first = True
    for arg in args:
        output += ('' if first else sep) + str(arg)
        first = False
    file.write(output + end)
print3(1, 2, 3,end=',')
```
`Output: 1,2,3`
### Chỉ sử dụng arguments
```python
import sys
def print3(*args, sep=' ', end='\n', file=sys.stdout):
    output = ''
    first = True
    for arg in args:
        output += ('' if first else sep) + str(arg)
        first= False
    file.write(output + end)
print3(99,101,end='bob')
```
`Output: 99 101bob`
### Tạo hàm mixmax
```python
def minmax(test, *args):
    res = args[0]
    for arg in args[1:]:
        if test(arg, res):# tương đương test(arg,res) !=None
            res = arg
    return res
def lessthan(x, y): 
    return x < y 
def grtrthan(x, y):
    return x > y
print(minmax(lessthan, 4, 2, 1, 5, 6, 3))
print(minmax(grtrthan, 4, 2, 1, 5, 6, 3))
```
Ouput:
```    
1
6
```









