Composite Design Pattern là một mẫu thiết kế (design pattern) thuộc nhóm mẫu cấu trúc (structural pattern) trong lĩnh vực lập trình. Mẫu này cho phép bạn xây dựng cấu trúc cây hierarchial với các đối tượng tương tự và định nghĩa một giao diện chung cho chúng. Composite cho phép các đối tượng đơn lẻ và nhóm đối tượng được xử lý một cách đồng nhất.

Trong C#, Composite Design Pattern thường được sử dụng để xây dựng cây đối tượng có cấu trúc phân cấp. Mẫu này giúp tạo ra một sự phân loại rõ ràng giữa các đối tượng lá (leaf objects) và các đối tượng phức hợp (composite objects). Các đối tượng lá là các thành phần cơ bản không có con và các đối tượng phức hợp là nhóm các đối tượng, cả lá và phức hợp, có thể chứa các thành phần con khác.

Dưới đây là một ví dụ về cách triển khai Composite Design Pattern trong C#:

```csharp
using System;
using System.Collections.Generic;

// Giao diện chung cho tất cả các thành phần
public interface IComponent
{
    void Operation();
}

// Đối tượng lá (leaf object)
public class Leaf : IComponent
{
    public void Operation()
    {
        Console.WriteLine("Leaf operation");
    }
}

// Đối tượng phức hợp (composite object)
public class Composite : IComponent
{
    private List<IComponent> components = new List<IComponent>();

    public void AddComponent(IComponent component)
    {
        components.Add(component);
    }

    public void RemoveComponent(IComponent component)
    {
        components.Remove(component);
    }

    public void Operation()
    {
        Console.WriteLine("Composite operation");
        foreach (var component in components)
        {
            component.Operation();
        }
    }
}

// Sử dụng Composite Design Pattern
class Program
{
    static void Main(string[] args)
    {
        // Tạo đối tượng lá
        var leaf1 = new Leaf();
        var leaf2 = new Leaf();

        // Tạo đối tượng phức hợp
        var composite1 = new Composite();
        var composite2 = new Composite();

        // Thêm các đối tượng lá vào đối tượng phức hợp
        composite1.AddComponent(leaf1);
        composite2.AddComponent(leaf2);

        // Thêm đối tượng phức hợp vào đối tượng phức hợp khác
        composite1.AddComponent(composite2);

        // Gọi phương thức Operation trên đối tượng phức hợp gốc
        composite1.Operation();

        /*
        Kết quả:
        Composite operation
        Leaf operation
        Composite operation
        Leaf operation
        */
    }
}
```

Trên đây là một ví dụ đơn giản về Composite Design Pattern trong C#. Bằng cách sử dụng mẫu thiết kế này, bạn có thể

 xây dựng các cây đối tượng phức tạp và xử lý chúng một cách đồng nhất. Mỗi đối tượng trong cây có thể được gọi để thực hiện một hành động cụ thể, không phụ thuộc vào việc đối tượng đó là lá hay phức hợp.
