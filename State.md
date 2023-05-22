State Design Pattern là một mẫu thiết kế hướng đối tượng trong lập trình, nó cho phép đối tượng thay đổi hành vi của mình dựa trên trạng thái nội tại của nó. Mẫu thiết kế này giúp tăng tính mô-đun, linh hoạt và dễ bảo trì cho mã nguồn.

Trong C#, State Design Pattern được triển khai bằng cách sử dụng các lớp và giao diện. Các yếu tố chính của mẫu thiết kế này là:
- Context: Đại diện cho đối tượng chứa trạng thái và triển khai các phương thức liên quan đến trạng thái. Nó giữ một tham chiếu đến một đối tượng trạng thái cụ thể.
- State: Đại diện cho giao diện hoặc lớp trạng thái cụ thể. Nó định nghĩa các phương thức mà context sẽ gọi khi nó ở trong trạng thái đó.
- ConcreteState: Các lớp cụ thể triển khai giao diện State. Mỗi lớp này đại diện cho một trạng thái cụ thể và triển khai các phương thức tương ứng.

Khi một sự kiện hoặc hành động xảy ra, context sẽ chuyển đổi trạng thái của nó bằng cách gọi phương thức tương ứng trên đối tượng trạng thái hiện tại. Các phương thức này có thể thay đổi trạng thái của context hoặc thực hiện các hành động khác.

Một ví dụ cụ thể để minh họa State Design Pattern trong C# là một ứng dụng quản lý tài khoản ngân hàng. Trạng thái của tài khoản có thể là "Mở", "Đóng" hoặc "Bị khóa". Mỗi trạng thái sẽ có các hành vi khác nhau như thực hiện giao dịch, rút tiền hoặc kiểm tra số dư.

Dưới đây là một mã nguồn minh họa cho ví dụ trên:

```csharp
// Giao diện định nghĩa các phương thức trạng thái
public interface IAccountState
{
    void Deposit(decimal amount);
    void Withdraw(decimal amount);
    void CheckBalance();
}

// Lớp trạng thái cụ thể "Mở"
public class OpenState : IAccountState
{
    private Account account;

    public OpenState(Account account)
    {
        this.account = account;
    }

    public void Deposit(decimal amount)
    {
        account.Balance += amount;
        Console.WriteLine($"{amount} deposited. Current balance: {account.Balance}");
    }

    public

 void Withdraw(decimal amount)
    {
        if (account.Balance >= amount)
        {
            account.Balance -= amount;
            Console.WriteLine($"{amount} withdrawn. Current balance: {account.Balance}");
        }
        else
        {
            Console.WriteLine("Insufficient balance.");
        }
    }

    public void CheckBalance()
    {
        Console.WriteLine($"Current balance: {account.Balance}");
    }
}

// Lớp trạng thái cụ thể "Đóng"
public class ClosedState : IAccountState
{
    public void Deposit(decimal amount)
    {
        Console.WriteLine("Account closed. Cannot deposit.");
    }

    public void Withdraw(decimal amount)
    {
        Console.WriteLine("Account closed. Cannot withdraw.");
    }

    public void CheckBalance()
    {
        Console.WriteLine("Account closed.");
    }
}

// Lớp trạng thái cụ thể "Bị khóa"
public class LockedState : IAccountState
{
    private Account account;

    public LockedState(Account account)
    {
        this.account = account;
    }

    public void Deposit(decimal amount)
    {
        Console.WriteLine("Account locked. Cannot deposit.");
    }

    public void Withdraw(decimal amount)
    {
        Console.WriteLine("Account locked. Cannot withdraw.");
    }

    public void CheckBalance()
    {
        Console.WriteLine("Account locked.");
    }
}

// Lớp chứa trạng thái và triển khai các phương thức liên quan
public class Account
{
    public decimal Balance { get; set; }
    private IAccountState currentState;

    public Account()
    {
        currentState = new OpenState(this);
    }

    public void Deposit(decimal amount)
    {
        currentState.Deposit(amount);
    }

    public void Withdraw(decimal amount)
    {
        currentState.Withdraw(amount);
    }

    public void CheckBalance()
    {
        currentState.CheckBalance();
    }

    public void ChangeState(IAccountState newState)
    {
        currentState = newState;
    }
}

// Sử dụng:
Account account = new Account();
account.Deposit(100);
account.Withdraw(50);

account.ChangeState(new ClosedState());
account.Deposit(100); // Kết quả: "Account closed. Cannot deposit."
account.CheckBalance(); // Kết quả: "Account closed."

account.ChangeState(new LockedState(account));
account.Withdraw(50); // Kết quả: "Account locked. Cannot withdraw."
```

Trong ví dụ trên, `Account` đóng vai trò là context và các lớp `OpenState`, `ClosedState`, `LockedState` đóng vai trò là các trạng thái cụ thể. Khi gọi các phương thức trên `Account`, chúng sẽ được chuyển tiếp đến trạng thái hiện tại để xử lý tương ứng.

State Design Pattern giúp tăng tính mô-đun và linh hoạt trong việc xử lý các trạng thái khác nhau của đối tượng, đồng thời giúp giảm sự phụ thuộc và dễ bảo trì.
