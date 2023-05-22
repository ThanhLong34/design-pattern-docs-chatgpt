Command Pattern là một mẫu thiết kế hành vi (behavioral design pattern) trong lập trình. Nó được sử dụng để đóng gói các yêu cầu hoặc hành động thành các đối tượng riêng biệt, từ đó cho phép chúng ta thực hiện các thao tác chức năng như một đối tượng độc lập.

Trong C#, Command Pattern được triển khai bằng cách sử dụng các lớp và giao diện. Các thành phần chính của Command Pattern bao gồm:

1. Command: Đây là một giao diện đại diện cho một yêu cầu hoặc hành động cụ thể. Giao diện này bao gồm một phương thức chung, ví dụ như `Execute()`, mà các lớp triển khai của nó sẽ cung cấp cài đặt cụ thể. 

```csharp
public interface ICommand
{
    void Execute();
}
```

2. Concrete Command: Đây là lớp triển khai của giao diện Command. Nó đóng gói một yêu cầu cụ thể và chứa các thông tin cần thiết để thực hiện yêu cầu đó. Lớp này cài đặt phương thức `Execute()` của giao diện Command.

```csharp
public class ConcreteCommand : ICommand
{
    private Receiver receiver;

    public ConcreteCommand(Receiver receiver)
    {
        this.receiver = receiver;
    }

    public void Execute()
    {
        receiver.Action();
    }
}
```

3. Invoker: Invoker là một đối tượng quản lý các đối tượng Command. Nó giữ một danh sách các Command và có thể gọi các phương thức `Execute()` của chúng khi cần thiết.

```csharp
public class Invoker
{
    private List<ICommand> commands = new List<ICommand>();

    public void AddCommand(ICommand command)
    {
        commands.Add(command);
    }

    public void ExecuteCommands()
    {
        foreach (ICommand command in commands)
        {
            command.Execute();
        }
    }
}
```

4. Receiver: Receiver là đối tượng thực hiện các hành động cụ thể khi được kích hoạt bởi một Command.

```csharp
public class Receiver
{
    public void Action()
    {
        // Thực hiện các hành động cụ thể
    }
}
```

Ví dụ sử dụng Command Pattern:

```csharp
Receiver receiver = new Receiver();
ICommand command = new ConcreteCommand(receiver);

Invoker invoker = new Invoker();
invoker.AddCommand(command);
invoker.ExecuteCommands();
```

Trong ví dụ này, chúng ta tạo một đối tượng Receiver để thực hiện hành động cụ thể, sau đó đóng gói hành động đó vào một đối tượng ConcreteCommand. Cuối cùng, chúng ta tạo một đối tượng Invoker, thêm ConcreteCommand vào danh sách các Command của nó và g

ọi phương thức `ExecuteCommands()` để thực hiện các Command đã thêm.

Command Pattern cho phép chúng ta tách biệt sự tương tác giữa người gửi yêu cầu (Invoker) và người nhận yêu cầu (Receiver). Nó cung cấp sự linh hoạt và dễ dàng mở rộng khi muốn thêm các yêu cầu hoặc hành động mới mà không cần sửa đổi Invoker hoặc Receiver.
