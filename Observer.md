Observer Design Pattern là một trong những mẫu thiết kế phần mềm (design pattern) thuộc nhóm hành vi (behavioral pattern) trong lập trình hướng đối tượng. Mẫu thiết kế này cho phép các đối tượng (observers) tự động nhận thông báo và cập nhật từ một đối tượng chủ đề (subject) khi có sự thay đổi trong trạng thái của nó. Điều này cho phép các đối tượng tương tác với nhau mà không cần biết thông tin chi tiết về nhau.

Trong C#, Observer Design Pattern có thể được triển khai bằng cách sử dụng một số thành phần cốt lõi như sau:

1. Subject (Chủ đề): Đây là đối tượng quản lý danh sách các observer và cung cấp các phương thức để thêm, xóa và thông báo cho các observer. Trong C#, một cách phổ biến để triển khai Subject là sử dụng một lớp trừu tượng hoặc giao diện để định nghĩa các phương thức chung.

```csharp
public abstract class Subject
{
    private List<Observer> observers = new List<Observer>();

    public void Attach(Observer observer)
    {
        observers.Add(observer);
    }

    public void Detach(Observer observer)
    {
        observers.Remove(observer);
    }

    public void Notify()
    {
        foreach (Observer observer in observers)
        {
            observer.Update();
        }
    }
}
```

2. Observer (Người quan sát): Đây là các đối tượng quan sát và nhận thông báo từ Subject. Trong C#, Observer thường được triển khai bằng cách sử dụng một lớp trừu tượng hoặc giao diện, và định nghĩa phương thức Update để xử lý thông báo từ Subject.

```csharp
public abstract class Observer
{
    public abstract void Update();
}
```

3. Concrete Subject (Chủ đề cụ thể): Lớp này triển khai các phương thức cụ thể của Subject và quản lý trạng thái của nó. Khi trạng thái thay đổi, nó gọi phương thức Notify để thông báo cho tất cả các Observer.

```csharp
public class ConcreteSubject : Subject
{
    private string state;

    public string State
    {
        get { return state; }
        set
        {
            state = value;
            Notify();
        }
    }
}
```

4. Concrete Observer (Người quan sát cụ thể): Lớp này triển khai phương thức Update để xử lý thông báo từ Subject. Nó có thể truy cập trực tiếp vào trạng thái của Subject để cập nhật và thực hiện các hành động phù hợp.

```csharp
public class ConcreteObserver : Observer
{
    private string name;
    private ConcreteSubject subject;

    public ConcreteObserver(string name,

 ConcreteSubject subject)
    {
        this.name = name;
        this.subject = subject;
    }

    public override void Update()
    {
        string subjectState = subject.State;
        Console.WriteLine("Observer {0} received the state update: {1}", name, subjectState);
    }
}
```

Ví dụ sử dụng Observer Design Pattern:

```csharp
ConcreteSubject subject = new ConcreteSubject();
ConcreteObserver observer1 = new ConcreteObserver("Observer 1", subject);
ConcreteObserver observer2 = new ConcreteObserver("Observer 2", subject);

subject.Attach(observer1);
subject.Attach(observer2);

subject.State = "State 1";
subject.State = "State 2";

subject.Detach(observer2);

subject.State = "State 3";
```

Kết quả:

```
Observer 1 received the state update: State 1
Observer 2 received the state update: State 1
Observer 1 received the state update: State 2
Observer 2 received the state update: State 2
Observer 1 received the state update: State 3
```

Trong ví dụ trên, khi trạng thái của ConcreteSubject thay đổi, tất cả các ConcreteObserver đính kèm đều nhận được thông báo và thực hiện hành động tương ứng.
