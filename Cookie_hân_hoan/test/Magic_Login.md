## CHALLENGE: MAGIC LOGIN 

Hé lu, nay chúng ta sẽ cùng đi giải challenge khá hay ho ở Cookiearena.

<img src ="img/img1.png">

Đập vào mặt là cái login page, điều đầu tiên thì cứ đi coi source code có chi thú vị hơm.

<img src ="img/img2.png">

Ở đây chúng ta có source code. Đụng tới code là mệt :))) Là câu nói mà những người khác sẽ nói chớ tui hỏng nói afaaaaaa.
Phân tích một chút về code.
 ```$usr = mysql_real_escape_string($_POST['username']); 
    $pas = hash('sha256', mysql_real_escape_string($_POST['password'])); 
 ```
Đoạn này là lấy input đầu vào nè, ở phần biến pas thì nó có thêm mã hóa sha256 nữa.

```
    if($pas == "0"){ 
        $_SESSION['logged'] = TRUE; 
        header("Location: upload.php"); // Modify to go to the page you would like 
        exit; 
    }else{ 
        header("Location: login_page.php"); 
        exit; 
    } 
}else{    //If the form button wasn't submitted go to the index page, or login page 
    header("Location: login_page.php");     
    exit; 
} 
```
Lệnh ```if``` để kiểm tra xem biến ```pas``` sau khi đã mã hóa có bằng 0 hay không.
Nếu bằng ```0``` thì chúng ta sẽ đến một trang mới là ```upload.php```, còn sai thì chúng ta vẫn ở lại trang login.

Vấn đề ở đây là làm thế nào để password nhập vào sau khi mã hóa lại cho bằng 0?
Ở đây chúng ta sẽ dùng ```magic hash``` or ```PHP hash "collisions"```. 
Nếu hiểu nôm na thì 1 text sau khi mã hóa sẽ cho ra 1 kết quả duy nhất và chúng nó không bằng nhau. Nhưng bằng một cách ```magic``` nào đó, sau khi tụi nó so sánh với nhau lại trả về kết quả ```true```. Ảo thật đấy.

Sử dụng [payload ở đây](https://github.com/spaze/hashes/blob/master/sha256.md) để bypass authentication nào. Chọn cái nào cũng được. Username thì nhập tùy ý vị huynh đài.

<img src="img/img3.png">

Sau khi đã đăng nhập thành công, lại đập vào mặt là 1 trang upload file.
Cứ đọc source code xem có chi thú zị.

<img src="img/img4.png">

Phân tích code 1 chút, ở đây chúng ta sẽ upload 1 file không quá 1Mb và sau khi đã thành công thì nó sẽ cung cấp cho ta 1 đường dẫn tới file chúng ta đã upload. Và đường dẫn đó sẽ là random. Tới đây hơi căng rồi đấy.

<img src="img/img5.png">

<img src="img/img6.png">

Bước đầu thì tui nghĩ chúng ta sẽ gửi tên file trùng với tên của ```flag.txt```, và từ đó nó sẽ đọc được file, nhưng tui đã quá nonnnnn :)))
Sau khi đọc lại code và tui có để ý đoạn code ni
``` $uploadedPath = "uploads/".rand().".".explode(".",$_FILES['fileData']['name'])[1];``` 
Nó có nghĩa là tạo ra 1 đường dẫn và tên file random rồi sau đó lấy cái extension của file mới gửi làm đuôi extension cho file mới.
Sao chúng ta không thử gửi file code lên web? Nó cũng có cấm đâu. Zị là viết 1 payload đơn giản để gửi lên

Đoạn payload mà tui dùng.

<img src="img/img7.png">

Sau khi gửi lên thì chúng ta sẽ có kết quả

<img src="img/img8.png">

## Tâm sự xíu
Đôi lúc học ATTT nó nhọc thiệt, mà đôi khi gặp challenge code cũng nản, nhưng làm chặp nó quen à, không giải được thì cứ đọc wu thôi. Hi vọng nếu ai có coi được wu ni thì cứ mạnh dạng làm mấy bài code, đọc hiểu hiểu là được, ai mượn code lại :))) và một lần nữa

## THANK YOU FOR LEARNING GUYS.

## PATIENCE IS THE KEY, SO KEEP TRYING EVERYDAY. LUV U <3

