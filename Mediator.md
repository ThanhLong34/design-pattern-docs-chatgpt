
Mediator Design Pattern là một mẫu thiết kế phần mềm thuộc nhóm hành vi (behavioral pattern) trong lập trình. Mẫu thiết kế này tập trung vào việc giảm sự phụ thuộc (coupling) giữa các thành phần trong một hệ thống phức tạp bằng cách định nghĩa một thành phần trung gian gọi là Mediator để quản lý tương tác giữa các thành phần khác nhau.

Mediator pattern giúp tạo ra một lớp trung gian (Mediator) để các đối tượng không cần phải giao tiếp trực tiếp với nhau. Thay vào đó, chúng giao tiếp thông qua Mediator. Điều này giảm sự phụ thuộc giữa các đối tượng và giúp chúng dễ dàng tái sử dụng và duy trì.

Trong C#, Mediator Design Pattern có thể được triển khai như sau:

1. Định nghĩa interface IMediator: Đây là giao diện cho Mediator và chứa các phương thức để giao tiếp với các đối tượng khác nhau trong hệ thống.

```csharp
public interface IMediator
{
    void SendMessage(string message, Colleague colleague);
}
```

2. Định nghĩa lớp Mediator: Lớp này triển khai giao diện IMediator và quản lý các đối tượng Colleague. Nó có thể chứa logic xử lý thông điệp và điều phối tương tác giữa các đối tượng.

```csharp
public class ConcreteMediator : IMediator
{
    private Colleague colleague1;
    private Colleague colleague2;

    public Colleague Colleague1
    {
        set { colleague1 = value; }
    }

    public Colleague Colleague2
    {
        set { colleague2 = value; }
    }

    public void SendMessage(string message, Colleague colleague)
    {
        if (colleague == colleague1)
        {
            colleague2.ReceiveMessage(message);
        }
        else if (colleague == colleague2)
        {
            colleague1.ReceiveMessage(message);
        }
    }
}
```

3. Định nghĩa lớp Colleague: Đây là lớp đại diện cho các đối tượng trong hệ thống. Chúng giao tiếp với nhau thông qua Mediator.

```csharp
public abstract class Colleague
{
    protected IMediator mediator;

    public Colleague(IMediator mediator)
    {
        this.mediator = mediator;
    }

    public abstract void SendMessage(string message);
    public abstract void ReceiveMessage(string message);
}
```

4. Triển khai lớp con của Colleague:

```csharp
public class ConcreteColleague1 : Colleague
{
    public ConcreteColleague1(IMediator mediator) : base(mediator)
    {
    }

    public override void SendMessage(string message)
    {
        mediator.SendMessage(message, this);
    }

    public override void ReceiveMessage(string message)
    {
        Console.WriteLine("ConcreteColleague1 received: " + message);
   

 }
}

public class ConcreteColleague2 : Colleague
{
    public ConcreteColleague2(IMediator mediator) : base(mediator)
    {
    }

    public override void SendMessage(string message)
    {
        mediator.SendMessage(message, this);
    }

    public override void ReceiveMessage(string message)
    {
        Console.WriteLine("ConcreteColleague2 received: " + message);
    }
}
```

5. Sử dụng Mediator trong chương trình:

```csharp
static void Main(string[] args)
{
    ConcreteMediator mediator = new ConcreteMediator();

    ConcreteColleague1 colleague1 = new ConcreteColleague1(mediator);
    ConcreteColleague2 colleague2 = new ConcreteColleague2(mediator);

    mediator.Colleague1 = colleague1;
    mediator.Colleague2 = colleague2;

    colleague1.SendMessage("Hello from Colleague1!");
    colleague2.SendMessage("Hello from Colleague2!");
}
```

Kết quả khi chạy chương trình sẽ là:

```
ConcreteColleague2 received: Hello from Colleague1!
ConcreteColleague1 received: Hello from Colleague2!
```

Ở đây, Mediator (ConcreteMediator) quản lý tương tác giữa hai đối tượng Colleague (ConcreteColleague1 và ConcreteColleague2). Các đối tượng không cần phải giao tiếp trực tiếp với nhau, mà thông qua Mediator để truyền thông điệp.
