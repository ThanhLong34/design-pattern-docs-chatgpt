Strategy Design Pattern là một trong các mẫu thiết kế phần mềm (design pattern) thuộc nhóm hành vi (behavioral patterns) trong lập trình hướng đối tượng. Mẫu này cho phép bạn xác định một tập hợp các thuật toán khác nhau và đóng gói chúng vào các đối tượng riêng biệt, từ đó có thể chọn lựa thuật toán phù hợp để sử dụng tại thời điểm thực thi.

Trong C#, Strategy Design Pattern thường được sử dụng để tách biệt logic xử lý từ các chi tiết cụ thể của thuật toán, từ đó giúp dễ dàng mở rộng, thay đổi và tái sử dụng code.

Dưới đây là cấu trúc của Strategy Design Pattern:

1. Strategy: Đây là một interface hoặc lớp trừu tượng chứa các phương thức mô tả các hành vi chung của các thuật toán. Ví dụ:

```csharp
public interface IStrategy
{
    void Execute();
}
```

2. Concrete Strategies: Đây là các lớp cụ thể thực hiện giao diện Strategy. Mỗi lớp cung cấp một cách thức cụ thể để thực hiện các thuật toán. Ví dụ:

```csharp
public class ConcreteStrategyA : IStrategy
{
    public void Execute()
    {
        // Thực hiện thuật toán A
    }
}

public class ConcreteStrategyB : IStrategy
{
    public void Execute()
    {
        // Thực hiện thuật toán B
    }
}
```

3. Context: Đây là lớp chứa một đối tượng Strategy và sử dụng nó để thực hiện công việc cụ thể. Lớp Context cho phép thay đổi Strategy tại thời điểm chạy. Ví dụ:

```csharp
public class Context
{
    private IStrategy _strategy;

    public Context(IStrategy strategy)
    {
        _strategy = strategy;
    }

    public void ExecuteStrategy()
    {
        _strategy.Execute();
    }
}
```

Với cấu trúc trên, ta có thể sử dụng Strategy Design Pattern như sau:

```csharp
// Sử dụng ConcreteStrategyA
var context = new Context(new ConcreteStrategyA());
context.ExecuteStrategy();

// Sử dụng ConcreteStrategyB
context = new Context(new ConcreteStrategyB());
context.ExecuteStrategy();
```

Khi chạy, kết quả sẽ tùy thuộc vào Strategy được chọn, và Context sẽ thực hiện công việc thông qua Strategy đó.

Strategy Design Pattern cho phép linh hoạt thay đổi thuật toán trong quá trình chạy, mở rộng thuật toán bằng cách thêm Concrete Strategies mới, và giúp tách biệt logic xử lý, dễ dàng bảo trì và tái sử dụng code

.
