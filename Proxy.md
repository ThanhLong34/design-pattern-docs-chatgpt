Proxy Pattern là một mẫu thiết kế (design pattern) trong lập trình được sử dụng để tạo ra một đối tượng proxy (đại diện) cho một đối tượng khác. Đối tượng proxy này cho phép bạn kiểm soát truy cập đến đối tượng gốc và cung cấp các chức năng bổ sung.

Trong C#, Proxy Pattern được triển khai bằng cách sử dụng một lớp proxy để đại diện cho đối tượng gốc và chuyển các yêu cầu từ client tới đối tượng gốc. Đối tượng proxy có cùng interface với đối tượng gốc, cho phép client giao tiếp với nó một cách như thể đang giao tiếp với đối tượng gốc.

Proxy Pattern thường được sử dụng trong các trường hợp sau:

1. Remote Proxy: Khi đối tượng gốc nằm ở một không gian bộ nhớ khác hoặc trên một máy chủ từ xa. Proxy Pattern cho phép bạn tạo ra một đối tượng proxy để đại diện cho đối tượng gốc và gửi yêu cầu tới đối tượng từ xa.

2. Virtual Proxy: Khi việc tạo đối tượng gốc mất nhiều tài nguyên hoặc thời gian. Proxy Pattern cho phép bạn tạo ra một đối tượng proxy để thực hiện các tác vụ như khởi tạo đối tượng gốc khi cần thiết.

3. Protection Proxy: Khi bạn muốn kiểm soát truy cập vào đối tượng gốc bằng cách thêm logic kiểm tra hoặc xác thực. Proxy Pattern cho phép bạn tạo ra một đối tượng proxy để kiểm soát việc truy cập đến đối tượng gốc.

Dưới đây là một ví dụ đơn giản về Proxy Pattern trong C#:

```csharp
// Interface chung cho đối tượng gốc và proxy
interface IImage
{
    void Display();
}

// Đối tượng gốc
class RealImage : IImage
{
    private string filename;

    public RealImage(string filename)
    {
        this.filename = filename;
        LoadFromDisk();
    }

    private void LoadFromDisk()
    {
        Console.WriteLine("Loading image from disk: " + filename);
    }

    public void Display()
    {
        Console.WriteLine("Displaying image: " + filename);
    }
}

// Proxy cho đối tượng gốc
class ProxyImage : IImage
{
    private string filename;
    private RealImage realImage;

    public ProxyImage(string filename)
    {
        this.filename = filename;
    }

    public void Display()
    {
        if (realImage == null)
        {
            realImage = new RealImage(filename);
        }
        realImage.Display();
    }
}

// Sử dụng Proxy Pattern
class Program
{
    static void Main(string[] args)
    {
        // Sử dụng đối tượng proxy để hi

ển thị hình ảnh
        IImage image = new ProxyImage("image.jpg");

        // Khi gọi phương thức Display(), hình ảnh chỉ được tải lên và hiển thị khi cần thiết
        image.Display();

        // Khi gọi lại phương thức Display(), hình ảnh đã được tải lên nên chỉ hiển thị mà không cần tải lại từ đĩa
        image.Display();

        Console.ReadLine();
    }
}
```

Trong ví dụ trên, `RealImage` là đối tượng gốc, thực hiện việc tải hình ảnh từ đĩa và hiển thị. `ProxyImage` là proxy cho `RealImage`, và chỉ tải và hiển thị hình ảnh khi cần thiết. Khi chạy chương trình, ta chỉ thấy thông điệp "Loading image from disk" xuất hiện một lần duy nhất, trong lần đầu tiên gọi phương thức `Display()`. Trong lần gọi phương thức thứ hai, hình ảnh đã được tải lên và hiển thị mà không cần tải lại từ đĩa.
