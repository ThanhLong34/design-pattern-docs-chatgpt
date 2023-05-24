Memento Design Pattern là một trong những mẫu thiết kế thuộc nhóm "Behavioral Patterns" (Mẫu hành vi) trong lĩnh vực lập trình. Mẫu này được sử dụng để lưu trữ và khôi phục trạng thái của một đối tượng mà không làm gián đoạn hoạt động của nó hoặc tiết lộ chi tiết triển khai.

Trong C#, Memento Design Pattern gồm ba thành phần chính: Originator (Nguyên tắc), Memento (Đối tượng lưu trữ) và Caretaker (Người chăm sóc).

1. Originator (Nguyên tắc): Đây là đối tượng cần lưu trữ và khôi phục trạng thái. Originator cung cấp các phương thức để tạo một Memento để lưu trữ trạng thái hiện tại của nó và khôi phục trạng thái từ một Memento đã cho. Nó cũng có thể trích xuất thông tin từ Memento.

```csharp
public class Originator
{
    private string state;

    public string State
    {
        get { return state; }
        set { state = value; }
    }

    public Memento CreateMemento()
    {
        return new Memento(state);
    }

    public void SetMemento(Memento memento)
    {
        state = memento.State;
    }
}
```

2. Memento (Đối tượng lưu trữ): Memento chứa trạng thái đã lưu trữ của Originator. Nó cung cấp phương thức để truy cập trạng thái đã lưu trữ, nhưng không tiết lộ chi tiết triển khai của nó.

```csharp
public class Memento
{
    private string state;

    public string State
    {
        get { return state; }
    }

    public Memento(string state)
    {
        this.state = state;
    }
}
```

3. Caretaker (Người chăm sóc): Caretaker là đối tượng chịu trách nhiệm lưu trữ và quản lý Memento. Nó chỉ cần giữ một tham chiếu đến Memento hiện tại, nhưng không can thiệp vào nội dung của Memento.

```csharp
public class Caretaker
{
    private Memento memento;

    public Memento Memento
    {
        get { return memento; }
        set { memento = value; }
    }
}
```

Để sử dụng Memento Design Pattern, bạn có thể thực hiện các bước sau:
1. Tạo một đối tượng Originator và thiết lập trạng thái ban đầu.
2. Tạo một đối tượng Caretaker và lưu trữ Memento từ Originator bằng cách gọi phương thức CreateMemento().
3. Thay đổi trạng thái của Originator.
4. Nếu bạn muốn khôi phục trạng

 thái ban đầu, gọi phương thức SetMemento() trên Originator với Memento đã lưu trữ từ Caretaker.

Dưới đây là một ví dụ minh họa:

```csharp
class Program
{
    static void Main(string[] args)
    {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        // Thiết lập trạng thái ban đầu của Originator
        originator.State = "Trạng thái ban đầu";
        Console.WriteLine("Trạng thái ban đầu: " + originator.State);

        // Lưu trữ trạng thái ban đầu
        caretaker.Memento = originator.CreateMemento();

        // Thay đổi trạng thái của Originator
        originator.State = "Trạng thái mới";
        Console.WriteLine("Trạng thái mới: " + originator.State);

        // Khôi phục trạng thái ban đầu
        originator.SetMemento(caretaker.Memento);
        Console.WriteLine("Trạng thái sau khi khôi phục: " + originator.State);
    }
}
```

Kết quả chạy chương trình sẽ là:

```
Trạng thái ban đầu: Trạng thái ban đầu
Trạng thái mới: Trạng thái mới
Trạng thái sau khi khôi phục: Trạng thái ban đầu
```

Như vậy, Memento Design Pattern cho phép bạn lưu trữ và khôi phục trạng thái của một đối tượng mà không làm gián đoạn hoạt động của nó. Điều này rất hữu ích khi bạn muốn ghi lại và hoàn tác các thao tác người dùng hoặc duy trì lịch sử thay đổi của đối tượng.

Ví dụ: Một ví dụ thực tế về việc sử dụng Memento Design Pattern trong C# có thể là hệ thống xử lý văn bản, trong đó người dùng có thể tạo, chỉnh sửa và khôi phục lại các phiên bản trước của văn bản.
