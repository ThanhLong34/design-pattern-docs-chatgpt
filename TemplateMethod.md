Template Method là một mẫu thiết kế (design pattern) thuộc nhóm mẫu thiết kế hành vi (behavioral design patterns) trong lập trình. Nó cho phép bạn xác định một khung (skeleton) cho một thuật toán trong một lớp cha, nhưng cho phép các lớp con triển khai cách thức cụ thể cho các bước của thuật toán đó.

Trong C#, Template Method được triển khai bằng cách sử dụng các lớp và phương thức ảo (virtual) trong lập trình hướng đối tượng. Các bước chung của thuật toán được xác định trong lớp cha, trong khi các bước cụ thể được triển khai trong các lớp con.

Dưới đây là một ví dụ đơn giản về cách triển khai Template Method Design Pattern trong C#:

```csharp
using System;

// Lớp cha chứa khung của thuật toán
abstract class AbstractClass
{
    // Phương thức Template Method
    public void TemplateMethod()
    {
        Step1();
        Step2();
        Step3();
    }

    // Các bước chung của thuật toán
    protected void Step1()
    {
        Console.WriteLine("Step 1");
    }

    protected void Step3()
    {
        Console.WriteLine("Step 3");
    }

    // Các bước cụ thể của thuật toán - để triển khai trong lớp con
    protected abstract void Step2();
}

// Lớp con 1 triển khai các bước cụ thể của thuật toán
class ConcreteClass1 : AbstractClass
{
    protected override void Step2()
    {
        Console.WriteLine("ConcreteClass1: Step 2");
    }
}

// Lớp con 2 triển khai các bước cụ thể khác của thuật toán
class ConcreteClass2 : AbstractClass
{
    protected override void Step2()
    {
        Console.WriteLine("ConcreteClass2: Step 2");
    }
}

class Program
{
    static void Main(string[] args)
    {
        AbstractClass class1 = new ConcreteClass1();
        AbstractClass class2 = new ConcreteClass2();

        // Gọi Template Method trên các đối tượng khác nhau
        class1.TemplateMethod();
        class2.TemplateMethod();

        Console.ReadKey();
    }
}
```

Kết quả khi chạy chương trình:

```
Step 1
ConcreteClass1: Step 2
Step 3
Step 1
ConcreteClass2: Step 2
Step 3
```

Trong ví dụ trên, lớp cha `AbstractClass` xác định khung của thuật toán thông qua phương thức `TemplateMethod()`, trong đó các bước chung `Step1()` và `Step3()` được triển khai sẵn. Các lớp con `ConcreteClass1` và `ConcreteClass2` triển khai bước cụ thể `Step2()` theo cách mà chúng muốn.

Qua việc sử dụng Template Method Design Pattern, bạn có thể x

ác định một khung chung cho một thuật toán và cho phép các lớp con triển khai các bước cụ thể mà không làm thay đổi cấu trúc của thuật toán. Điều này giúp tăng tính mô đun hóa và tái sử dụng trong mã nguồn của bạn.
