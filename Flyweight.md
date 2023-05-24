Flyweight là một mẫu thiết kế (design pattern) trong lập trình, nó được sử dụng để tối ưu hóa việc sử dụng bộ nhớ bằng cách chia sẻ các đối tượng có tính chất giống nhau. Mẫu thiết kế Flyweight (hay còn gọi là Lightweight) thường được sử dụng trong các hệ thống có số lượng lớn các đối tượng và việc tạo ra mỗi đối tượng mới có thể gây chiếm dụng bộ nhớ quá mức hoặc tốn thời gian.

Trong C#, Flyweight Design Pattern có thể được triển khai bằng cách sử dụng các lớp và interface để đại diện cho đối tượng và các đối tượng tương đồng. Các đối tượng tương đồng được chia sẻ thông qua một Factory hoặc một bộ đếm (pool) để tránh việc tạo ra quá nhiều đối tượng mới.

Dưới đây là một ví dụ về cách triển khai Flyweight Design Pattern trong C#:

```csharp
// Interface đại diện cho các đối tượng tương đồng
interface IFlyweight
{
    void Operation();
}

// Lớp cụ thể của đối tượng tương đồng
class ConcreteFlyweight : IFlyweight
{
    private string intrinsicState;

    public ConcreteFlyweight(string intrinsicState)
    {
        this.intrinsicState = intrinsicState;
    }

    public void Operation()
    {
        Console.WriteLine("Operation with intrinsic state: " + intrinsicState);
    }
}

// Factory để quản lý việc chia sẻ các đối tượng
class FlyweightFactory
{
    private Dictionary<string, IFlyweight> flyweights = new Dictionary<string, IFlyweight>();

    public IFlyweight GetFlyweight(string key)
    {
        if (flyweights.ContainsKey(key))
        {
            return flyweights[key];
        }
        else
        {
            IFlyweight flyweight = new ConcreteFlyweight(key);
            flyweights.Add(key, flyweight);
            return flyweight;
        }
    }
}

// Sử dụng Flyweight Design Pattern
class Program
{
    static void Main(string[] args)
    {
        FlyweightFactory factory = new FlyweightFactory();

        IFlyweight flyweight1 = factory.GetFlyweight("key1");
        flyweight1.Operation(); // Kết quả: Operation with intrinsic state: key1

        IFlyweight flyweight2 = factory.GetFlyweight("key2");
        flyweight2.Operation(); // Kết quả: Operation with intrinsic state: key2

        IFlyweight flyweight3 = factory.GetFlyweight("key1");
        flyweight3.Operation(); // Kết quả: Operation with intrinsic state: key1 (sử dụng lại đối tượng đã được tạo trước đó)

        Console.ReadLine();
    }
}
```

Trong ví dụ trên, `IFlyweight` đại diện cho giao diện của các đối tượng tương đồng và `ConcreteFlyweight` là lớp cụ thể triển khai giao diện

 đó. `FlyweightFactory` quản lý việc chia sẻ các đối tượng thông qua một từ điển. Khi cần sử dụng một đối tượng, Factory kiểm tra xem nó đã tồn tại trong từ điển chưa. Nếu chưa, nó sẽ tạo mới và thêm vào từ điển. Nếu đã tồn tại, nó sẽ trả về đối tượng đã tồn tại. Kết quả là các đối tượng có cùng tính chất (intrinsic state) được chia sẻ và sử dụng lại, giúp tiết kiệm bộ nhớ và tăng hiệu năng trong hệ thống.
 
 Ví dụ: Một ví dụ thực tế của Flyweight Design Pattern là việc quản lý các biểu đồ trong một ứng dụng vẽ đồ thị. Trên một bảng vẽ, người dùng có thể tạo ra nhiều hình dạng khác nhau như hình vuông, hình tròn, hình tam giác, v.v. Mỗi hình dạng có các thuộc tính riêng như màu sắc, độ dày nét vẽ, v.v.

Trong trường hợp này, sử dụng Flyweight Design Pattern có thể giúp tối ưu việc sử dụng bộ nhớ bằng cách chia sẻ các thuộc tính giống nhau giữa các hình dạng. Các đối tượng hình dạng sẽ được chia sẻ thông qua một Factory, đồng thời được lưu trữ trong một bộ đếm (pool) để quản lý.
