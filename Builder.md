Builder Design Pattern là một mẫu thiết kế (design pattern) trong lập trình phần mềm. Nó thuộc nhóm mẫu thiết kế tạo (creational design patterns) và được sử dụng để xây dựng các đối tượng phức tạp từ các thành phần đơn giản và tương thích.

Mục đích chính của Builder Design Pattern là tách rời quá trình xây dựng đối tượng (construction) của một lớp khỏi việc biểu diễn cấu trúc của nó (representation). Điều này cho phép cùng một quá trình xây dựng có thể tạo ra các biểu diễn khác nhau của một đối tượng.

Trong C#, Builder Design Pattern thường được sử dụng khi muốn xây dựng các đối tượng phức tạp có nhiều thuộc tính và các bước xây dựng phức tạp. Mẫu thiết kế này bao gồm các thành phần chính sau:

1. Builder: Đây là một giao diện hoặc một lớp trừu tượng định nghĩa các phương thức để xây dựng các phần tử của đối tượng cuối cùng.

2. ConcreteBuilder: Đây là lớp cụ thể triển khai giao diện Builder và cung cấp các phương thức cụ thể để xây dựng các phần tử của đối tượng cuối cùng.

3. Director: Đây là lớp hoặc giao diện điều khiển quá trình xây dựng của đối tượng cuối cùng. Nó sử dụng một đối tượng Builder để xây dựng đối tượng cuối cùng theo các bước cụ thể.

4. Product: Đây là đối tượng cuối cùng được xây dựng. Nó chứa các thành phần xây dựng bởi ConcreteBuilder và được sử dụng trong các bước xử lý khác nhau.

Cách sử dụng Builder Design Pattern trong C#:

1. Định nghĩa giao diện Builder và định nghĩa các phương thức cần thiết để xây dựng các phần tử của đối tượng cuối cùng.

2. Triển khai lớp ConcreteBuilder để cung cấp các phương thức cụ thể để xây dựng các phần tử của đối tượng cuối cùng.

3. Định nghĩa lớp Director và sử dụng đối tượng Builder để thực hiện các bước xây dựng đối tượng cuối cùng.

4. Xây dựng đối tượng cuối cùng bằng cách gọi các phương thức từ lớp Director.



5. Trả về đối tượng cuối cùng từ phương thức xây dựng của lớp Director.

Builder Design Pattern giúp cải thiện tính linh hoạt và mở rộng của mã nguồn, cho phép xây dựng các đối tượng phức tạp một cách dễ dàng và có thể tái sử dụng. Nó cũng giúp tránh việc xây dựng các đối tượng có nhiều tham số truyền vào trong hàm khởi tạo (constructor), giúp mã nguồn dễ đọc và bảo trì hơn.

Để minh họa cách sử dụng Builder Design Pattern trong một ví dụ thực tế, hãy xem xét một trường hợp xây dựng đối tượng "Pizza" với các thuộc tính như kích thước, loại bột và các topping.

Đầu tiên, chúng ta định nghĩa giao diện Builder có các phương thức để xây dựng các phần tử của đối tượng Pizza:

```csharp
public interface IPizzaBuilder
{
    void SetSize(string size);
    void SetCrust(string crust);
    void AddTopping(string topping);
    Pizza GetPizza();
}
```

Tiếp theo, chúng ta triển khai lớp ConcreteBuilder để xây dựng các phần tử của đối tượng Pizza:

```csharp
public class PizzaBuilder : IPizzaBuilder
{
    private Pizza pizza;

    public PizzaBuilder()
    {
        pizza = new Pizza();
    }

    public void SetSize(string size)
    {
        pizza.Size = size;
    }

    public void SetCrust(string crust)
    {
        pizza.Crust = crust;
    }

    public void AddTopping(string topping)
    {
        pizza.Toppings.Add(topping);
    }

    public Pizza GetPizza()
    {
        return pizza;
    }
}
```

Tiếp theo, chúng ta định nghĩa lớp Director để điều khiển quá trình xây dựng đối tượng Pizza:

```csharp
public class PizzaDirector
{
    public Pizza BuildPizza(IPizzaBuilder builder)
    {
        builder.SetSize("Large");
        builder.SetCrust("Thin");
        builder.AddTopping("Cheese");
        builder.AddTopping("Pepperoni");
        builder.AddTopping("Mushrooms");

        return builder.GetPizza();
    }
}
```

Cuối cùng, chúng ta có đối tượng Pizza:

```csharp
public class Pizza
{
    public string Size { get; set; }
    public string Crust { get; set; }
    public List<string> Toppings { get; set; }

    public Pizza()
    {
        Toppings = new List<string>();
    }

    public void Display()
    {
        Console.WriteLine($"Size: {Size}");
        Console.WriteLine($"Crust: {Crust}");
        Console.WriteLine("Toppings:");
        foreach (string topping in Toppings)
        {
            Console.WriteLine(topping);
        }
    }
}
```

Bây giờ chúng ta có thể sử dụng Builder Design Pattern để xây dựng một đối tượng Pizza:

```csharp
PizzaBuilder builder = new PizzaBuilder();
PizzaDirector director = new PizzaDirector();

Pizza pizza = director.BuildPizza(builder);
pizza.Display();
```

Kết quả sẽ là một đối tượng Pizza được xây dựng với kích thước là "Large", loại bột là "Thin" và các topping bao gồm "Cheese", "Pepperoni" và "Mushrooms".
