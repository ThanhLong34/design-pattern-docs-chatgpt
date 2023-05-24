Mẫu thiết kế Bridge là một mẫu thiết kế cấu trúc (structural design pattern) trong lập trình hướng đối tượng (OOP). Mẫu thiết kế này cho phép bạn tách biệt một lớp giao diện (abstraction) khỏi các lớp cụ thể thực hiện (implementations). Điều này giúp bạn có thể thay đổi lớp cụ thể mà không ảnh hưởng đến các lớp sử dụng lớp giao diện.

Trong C#, bạn có thể triển khai Bridge Design Pattern bằng cách sử dụng các lớp và giao diện. Hãy xem ví dụ sau:

Đầu tiên, chúng ta định nghĩa một giao diện "Implementor" để đại diện cho các lớp cụ thể thực hiện:

```csharp
public interface IImplementor
{
    void OperationImpl();
}
```

Tiếp theo, chúng ta có lớp giao diện "Abstraction" sử dụng giao diện "Implementor" để thực hiện một phương thức:

```csharp
public abstract class Abstraction
{
    protected IImplementor implementor;

    public Abstraction(IImplementor implementor)
    {
        this.implementor = implementor;
    }

    public abstract void Operation();
}
```

Sau đó, chúng ta triển khai các lớp cụ thể thực hiện "ImplementorA" và "ImplementorB" từ giao diện "IImplementor":

```csharp
public class ImplementorA : IImplementor
{
    public void OperationImpl()
    {
        Console.WriteLine("Implementor A operation");
    }
}

public class ImplementorB : IImplementor
{
    public void OperationImpl()
    {
        Console.WriteLine("Implementor B operation");
    }
}
```

Cuối cùng, chúng ta triển khai lớp "RefinedAbstraction" từ lớp "Abstraction" và triển khai phương thức "Operation" bằng cách sử dụng lớp cụ thể thực hiện tương ứng:

```csharp
public class RefinedAbstraction : Abstraction
{
    public RefinedAbstraction(IImplementor implementor) : base(implementor)
    {
    }

    public override void Operation()
    {
        implementor.OperationImpl();
    }
}
```

Bây giờ, chúng ta có thể sử dụng các lớp này như sau:

```csharp
// Tạo đối tượng RefinedAbstraction với ImplementorA
Abstraction abstraction = new RefinedAbstraction(new ImplementorA());
abstraction.Operation(); // Output: Implementor A operation

// Tạo đối tượng RefinedAbstraction với ImplementorB
abstraction = new RefinedAbstraction(new ImplementorB());
abstraction.Operation(); // Output: Implementor B operation
```

Khi chúng ta thay đổi lớp cụ thể thực hiện (implementor), ví dụ như từ "ImplementorA" sang "ImplementorB", lớp giao diện "

Abstraction" vẫn không bị ảnh hưởng và vẫn hoạt động như thông thường.

Mẫu thiết kế Bridge giúp chúng ta tách biệt các thành phần và giảm sự phụ thuộc giữa chúng. Điều này mang lại sự linh hoạt và dễ dàng mở rộng trong quá trình phát triển phần mềm.

Ví dụ: Trong một công ty có nhiều loại nhân viên. Mỗi loại nhân viên có một cách tính lương khác nhau. Chương trình quản lý nhân viên của bạn sẽ tính toán lương cho một nhân viên như thế nào họ chuyển từ loại này sang loại khác(hoặc chuyển từ phòng ban này sang phòng ban khác,). Ví dụ: Khi bạn apply vào vị trí developer của một công ty phần mềm, khi bắt đầu làm thì bạn là junior, một bậc cao hơn là senior, và cao hơn nữa là vai trò leader.Mỗi lần “lên cấp” như vậy là một lần thay đổi công thức tính lương.

Một ví dụ thực tế về việc sử dụng mẫu thiết kế Bridge có thể là hệ thống đồ họa trong một ứng dụng đa nền tảng. Giả sử bạn đang phát triển một ứng dụng vẽ đồ họa và bạn muốn hỗ trợ nhiều nền tảng như Windows, macOS và Linux.
Trong trường hợp này, bạn có thể sử dụng mẫu thiết kế Bridge để tách biệt lớp giao diện đồ họa (abstraction) khỏi các lớp cụ thể thực hiện (implementations) cho từng nền tảng. Điều này giúp bạn có thể dễ dàng thay đổi hoặc mở rộng hỗ trợ cho các nền tảng mới mà không ảnh hưởng đến phần còn lại của ứng dụng.
