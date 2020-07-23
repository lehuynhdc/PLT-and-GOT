# PLT-and-GOT(hướng dẫn của mấy anh khóa trước)

* Procedure Linkage Table (PLT) là một cái bảng chứa các địa chỉ hàm trong chương trình khi compile, 
các hàm trong bảng này khi được gọi đến có nhiệm vụ trỏ tới hàm tương ứng trong Global Offset Table ( GOT) hay còn gọi là bảng GO, 
bảng này chứa các địa chỉ hàm trong thư viện, thư viện này được liên kết với chương trình thông qua khai báo #include 
Việc tạo ra 2 bảng này mục đích như sau:
PLT sẽ giúp cho chương trình gọi tới các hàm mặc dù các hàm này nó thật sự đang ở bên thư viện, việc nó làm là liên kết tới đó thôi, 
nó sẽ tìm đến địa chỉ thật sự của hàm trong thư viện bằng _look_up__() như em nói, sau đó, để những lần sau đỡ mất thời gian thì nó 
lưu lại địa chỉ của hàm thật sự trong thư viện đó vào trong GOT, bảng này chỉ lưu địa chỉ thật việc còn lại là nhảy tới địa chỉ thật đó và thực thi, 
còn địa chỉ hàm trong PLT là để linkage tức liên kết tới chỗ thật mà  thôi

* cứ tưởng tượng : plt là cái số điện thoại, còn cái số điện thoại đó khi gọi tới, đường truyền sẽ kết nối như thế nào, dẫn tới ai thì là got.
Plt : nó lưu lại địa chỉ của GOT ( tức là nó lưu cái số điện thoại của người A nào đó ) 
Got: trách nhiệm của got là khi được gọi đến, nó phải tìm cho được địa chỉ của cái hàm mà nó được trỏ đến ( tức là nó phải truyền tín hiệu đến đt người A) ,
còn nếu mà ở lần đầu tiên nó chưa tìm được cái điện thoại của người A, thì nó phải đi tìm, tìm sao cho trúng được cái điện thoại đó, xong nó nhớ,
nhớ rằng cái điện thoại đó-có số đó. mỗi lần gọi số đó chỉ cần bay vèo tới cái điện thoại đó, khỏi phải đi tìm trong hàng tỉ tỉ cái điện thoại khác.

* mỗi khi mà chương trình chạy, thì nó dùng mấy cái hàm puts, gets. 
---- lúc này plt, got đã hình thành rồi: nó chứa những cái hàm được sử dụng trong chương trình ----

vậy mấy cái hàm đó ở đâu? trong chương trình không có( đối với dynamic linked) , nên nó mới phải tìm trong libc mà nó được liên kết, lấy ra để nó sử dụng. 

thì lúc đó got làm nhiệm vụ chính của nó:
ví dụ 1 hàm puts: nó phải chứa địa chỉ của  hàm puts trong thư viện, để khi ta gọi hàm puts, plt sẽ tìm tới cái got mà nó trỏ tới, từ cái got đó nó mới gọi tới puts.
Nhưng khi mới hình thành thì got nó chẳng có liền cái địa chỉ puts đâu, chưa ai bắt nó phải đi tìm hết. Nên nó trỏ tới 1 hàm, _look_up__( ) , 
khi hàm này được gọi, nó tìm cái địa chỉ puts trong libc, rồi trả về cho got, thế là từ đó got chứa địa chỉ của puts.
đơn giản vậy thôi á
Sau này sẽ có nhiều bài liên quan đến got, plt. Xài riết 1 ngày bỗng gặp bài chẳng thấy plt đâu, chẳng thấy got đâu thì lại khóc ròng. nên phải hiểu, 
dù debugger không có,thì nó vẫn tồn tại.
