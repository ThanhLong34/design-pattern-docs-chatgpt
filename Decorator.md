Decorator Design Pattern là một mẫu thiết kế (design pattern) trong lập trình, thuộc nhóm các mẫu thiết kế cấu trúc (structural design patterns). Mục tiêu của Decorator Design Pattern là định nghĩa một cách linh hoạt những chức năng mở rộng cho một đối tượng mà không làm thay đổi cấu trúc của lớp gốc.

Trong C#, Decorator Design Pattern cho phép bạn bọc (wrap) một đối tượng bên trong một đối tượng decorator để mở rộng hoặc thay đổi hành vi của đối tượng ban đầu mà không ảnh hưởng đến các đối tượng khác trong cùng một lớp.

Cấu trúc của Decorator Design Pattern bao gồm các thành phần sau:
- Component: là một interface hoặc lớp trừu tượng (abstract class) định nghĩa các phương thức chung cho các đối tượng gốc và decorator.
- ConcreteComponent: là lớp cài đặt giao diện Component. Đây là đối tượng ban đầu mà chúng ta muốn mở rộng hoặc thay đổi.
- Decorator: là một lớp trừu tượng (abstract class) kế thừa từ Component. Nó cũng chứa một tham chiếu đến một đối tượng Component. Decorator có thể thêm hoặc sửa đổi hành vi của Component.
- ConcreteDecorator: là lớp cài đặt giao diện Decorator. Nó bao gồm một đối tượng Component và triển khai các phương thức của Decorator. Nó cũng có thể thực hiện thêm logic bổ sung trước hoặc sau khi gọi đến phương thức của Component.

Dưới đây là một ví dụ minh họa Decorator Design Pattern trong C#:

```csharp
// Component
public interface ICar
{
    string GetDescription();
    double GetCost();
}

// ConcreteComponent
public class BasicCar : ICar
{
    public string GetDescription()
    {
        return "Basic Car";
    }

    public double GetCost()
    {
        return 10000;
    }
}

// Decorator
public abstract class CarDecorator : ICar
{
    protected ICar _car;

    public CarDecorator(ICar car)
    {
        _car = car;
    }

    public virtual string GetDescription()
    {
        return _car.GetDescription();
    }

    public virtual double GetCost()
    {
        return _car.GetCost();
    }
}

// ConcreteDecorator
public class LuxuryCar : CarDecorator
{
    public LuxuryCar(ICar car) : base(car)
    {
    }

    public override string GetDescription()
    {
        return base.GetDescription() + ", Luxury Features";
    }

    public override double GetCost()
    {
        return base.GetCost() + 5000;
    }
}

// ConcreteDecorator
public class SportsCar : CarDecorator
{
    public SportsCar(ICar car) : base(car)
    {
    }

    public override

 string GetDescription()
    {
        return base.GetDescription() + ", Sports Features";
    }

    public override double GetCost()
    {
        return base.GetCost() + 2000;
    }
}

// Usage
class Program
{
    static void Main(string[] args)
    {
        // Tạo một đối tượng cơ bản
        ICar basicCar = new BasicCar();
        Console.WriteLine(basicCar.GetDescription()); // Output: Basic Car
        Console.WriteLine(basicCar.GetCost()); // Output: 10000

        // Bọc đối tượng cơ bản vào các decorator để mở rộng chức năng
        ICar sportsLuxuryCar = new SportsCar(new LuxuryCar(new BasicCar()));
        Console.WriteLine(sportsLuxuryCar.GetDescription()); // Output: Basic Car, Luxury Features, Sports Features
        Console.WriteLine(sportsLuxuryCar.GetCost()); // Output: 17000
    }
}
```

Trong ví dụ trên, chúng ta có một đối tượng `BasicCar` làm đối tượng gốc và các decorator `LuxuryCar` và `SportsCar` để mở rộng chức năng. Khi chạy chương trình, chúng ta có thể thấy đối tượng cuối cùng `sportsLuxuryCar` có mô tả là "Basic Car, Luxury Features, Sports Features" và giá trị là 17000.

Decorator Design Pattern cho phép chúng ta mở rộng chức năng của một đối tượng một cách linh hoạt bằng cách bọc nó vào các decorator khác nhau. Điều này giúp chúng ta thay đổi hành vi của đối tượng mà không làm thay đổi cấu trúc của nó, đồng thời giúp tăng tính linh hoạt và dễ dàng bảo trì của mã nguồn.
