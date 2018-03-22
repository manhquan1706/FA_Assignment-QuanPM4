# Checklist_Javascript_04_QuanPM4

1 Async
1.1 Sync vs Async
- Synchronous có nghĩa là xử lý đồng bộ, chương trình sẽ chạy theo từng bước và chỉ khi nào bước 1 thực hiện xong thì mới nhảy sang bước 2, khi nào chương trình này chạy xong mới nhảy qua chương trình khác. Đây là nguyên tắc cơ bản trong lập trình là khi biên dịch các đoạn mã thì trình biên dịch sẽ biên dịch theo thứ tự từ trên xuống dưới, từ trái qua phải và chỉ khi nào biên dịch xong dòng thứ nhất mới nhảy sang dòng thứ hai, điều này sẽ sinh ra một trạng thái ta hay gọi là trạng thái chờ. Ví dụ trong quy trình sản xuất dây chuyền công nghiệp được coi là một hệ thống xử lý đồng bộ.

- Ngược lại với Synchronous thì Asynchronous là xử lý bất động bộ, nghĩa là chương trình có thể nhảy đi bỏ qua một bước nào đó, vì vậy Asynchronous được ví như một chương trình hoạt động không chặt chẽ và không có quy trình nên việc quản lý rất khó khăn. Nếu một hàm A phải bắt buộc chạy trước hàm B thì với Asynchronous sẽ không thể đảm bảo nguyên tắc này luôn đúng.
- Theo em, Javascript là một ngôn ngữ của xử lý bất đồng bộ.
1.2 setTimeout
```
console.log('Hi');
setTimeout(function () {
  console.log('there');
}, 1000);
```
Đoạn code trên đầu tiên ở màn hình console.log sẽ in ra kết quả là Hi. Sau đó ta phải chờ 1 giây thì sẽ in ra tiếp kết quả thứ 2 là there.
```
console.log('Hi');
setTimeout(function () {
  console.log('there');
}, 0);
console.log('Hi again');
```
- Ở ví dụ trên, em thấy trình duyệt in ra kết quả từ trên xuống dưới là Hi => Hi again nhưng bỏ qua bước console.log thứ 2 và in ra there là kết quả cuối cùng.
1.3 Event Loop
- Theo ý hiểu của em thì ở đoạn code trên (1) thì kết quả in ra sẽ là từ trên xuống dưới. Bắt đầu là console.log ra Hi, và tiếp theo console.log sẽ ra kết quả cuối cùng là (2).
- Còn ở đoạn code (2) thì khi chạy đoạn code kết quả cũng vẫn chạy từ trên xuống dưới, kết quả đầu tiên là Hi, nhưng ở console.log thứ 2 there được đưa vào hàng chờ nên kết quả thứ 2 sẽ là Hi again và sau đó there mới là kết quả cuối cùng được in ra.
1.4 Callbacks
```
// (1)
setTimeout(function () {
  // (2)
}, 1000);
// (3)
```
- Đoạn code trên sẽ chạy //1 đầu tiên sau đó đến //3 và cuối cùng là //2 vì setTimeout của //2 là 1000 nên đoạn code //2 sẽ bị trễ 1s.
1.4.1 Nested/ Chained Callbacks
```
// (0)
var btn = document.getElementById('btn');
btn.addEventListener('click', function () {
  // (1)
  setTimeout(function () {
    // (2)
  }, 1000);
  // (3)
});
```
- Đoạn code trên sẽ chạy đồng bộ từ //0 > //1 > //3 và sẽ bất đồng bộ ở //2 vì 2 setTimeout có độ trễ là 1s và được đưa vào hàm chờ . Nên thứ tự kết quả in ra sẽ là //0 > //1 > //3 > //2.

1.5 Promises
- Promise là một đối tượng đặc biệt dùng cho các xử lý bất đồng bộ. Nó đại diện cho một xử lý bất đồng bộ và chứa kết quả cũng như các lỗi xảy ra từ xử lý bất đồng bộ đó.
 - Future value là giá trị trong tương lai sẽ trả về.
- Promise value là giá trị khi đến thời điểm trả về sẽ là thành công hoặc là thất bại
- Promise Events là sự kiện trả về là resolve hoặc reject.
- Để lấy Promise value dùng .then sau đó tạo 1 function để nhận lấy giá trị trả về. 
- Handle error in Promise là sử dụng reject để trả về 1 lý do lỗi hoặc xử lý lỗi.
- Chain Promises là nối các .then với nhau để trả về các chuỗi.
- Promise.all 
Phương thức này được sử dụng khi ta đợi các Promise kết thúc. Trả ra một promise đại diện cho tất cả các kết quả thu được từ các promise ở trong iterable sau khi tất cả các promise này kết thúc xử lý thành công. Hoặc, trả ra một promise đại diện cho lỗi thực thi ngay khi một promise nào đó kết thúc lỗi.
- Promise.race
Trả ra một promise ngay sau khi một trong các promise trong iterable kết thúc xử lý. Tức là dù kết quả thu được là lỗi hay thành công thì ta cũng sẽ trả ngay ra một promise mới và promise mới này sẽ chứa kết quả của promise được kết thúc đầu tiên.
- Finally
Gắn một handler với promise và trả lại một promise mới được giải quyết khi promise ban đầu được giải quyết. Handler được gọi là khi promise được giải quyết, dù đã được thực hiện hay bị từ chối.




