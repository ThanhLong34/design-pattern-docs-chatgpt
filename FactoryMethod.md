Factory Method Design Pattern là một mẫu thiết kế phần mềm thuộc nhóm Creational Patterns trong lập trình hướng đối tượng. Mẫu này cho phép chúng ta tạo ra các đối tượng mà không cần chỉ định trực tiếp lớp cụ thể của chúng. Thay vào đó, nó tạo ra đối tượng thông qua một phương thức gọi là "factory method".

Trong C#, Factory Method Design Pattern được triển khai bằng cách tạo ra một lớp trừu tượng gọi là "Creator", chứa phương thức factory method. Lớp Creator định nghĩa phương thức để tạo ra đối tượng, nhưng không cung cấp cài đặt cụ thể cho phương thức này. Thay vào đó, các lớp con của Creator sẽ thừa kế từ Creator và cung cấp cài đặt cụ thể cho phương thức factory method.

Dưới đây là một ví dụ về cách triển khai Factory Method Design Pattern trong C#:

```csharp
// Creator abstract class
abstract class Creator
{
    public abstract Product FactoryMethod(); // Factory Method

    public void SomeOperation()
    {
        // Gọi factory method để tạo đối tượng
        Product product = FactoryMethod();

        // Sử dụng đối tượng đã tạo
        product.Operation();
    }
}

// Product abstract class
abstract class Product
{
    public abstract void Operation();
}

// ConcreteCreator class
class ConcreteCreator : Creator
{
    public override Product FactoryMethod()
    {
        return new ConcreteProduct();
    }
}

// ConcreteProduct class
class ConcreteProduct : Product
{
    public override void Operation()
    {
        Console.WriteLine("ConcreteProduct.Operation() called");
    }
}

// Sử dụng mẫu Factory Method
class Program
{
    static void Main(string[] args)
    {
        Creator creator = new ConcreteCreator();
        creator.SomeOperation();

        // Kết quả:
        // ConcreteProduct.Operation() called
    }
}
```

Trong ví dụ trên, lớp Creator là một lớp trừu tượng có một phương thức FactoryMethod. Lớp ConcreteCreator là một lớp con của Creator và triển khai phương thức FactoryMethod để tạo ra một đối tượng của ConcreteProduct. Lớp ConcreteProduct là một lớp con của Product và triển khai phương thức Operation.

Khi chạy, chương trình tạo một đối tượng của ConcreteCreator và gọi phương thức SomeOperation. Phương thức này sẽ sử dụng phương thức FactoryMethod để tạo ra một đối tượng của ConcreteProduct và gọi phương thức Operation của nó.

Factory Method Design Pattern cho phép chúng ta tách rời việc tạo đối tượng và sử dụng đối tượng, giúp linh hoạt trong việc mở rộng và thay đổi lớp cụ thể của đối tượng mà không ảnh hưởng

 đến mã gọi.
