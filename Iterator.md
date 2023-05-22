Iterator Design Pattern là một mẫu thiết kế phần mềm thuộc nhóm Behavioral Patterns. Nó cho phép duyệt qua một tập hợp các phần tử mà không cần tiết lộ cấu trúc nội bộ của tập hợp đó.

Trong C#, Iterator Design Pattern được triển khai bằng cách sử dụng interface `IEnumerable` và `IEnumerator` hoặc sử dụng từ khóa `yield`.

1. Triển khai Iterator Design Pattern bằng `IEnumerable` và `IEnumerator`:
   - `IEnumerable` là một interface định nghĩa một phương thức `GetEnumerator()` trả về một đối tượng `IEnumerator`.
   - `IEnumerator` là một interface định nghĩa các phương thức `MoveNext()`, `Reset()` và thuộc tính `Current` để duyệt qua các phần tử trong tập hợp.

   Ví dụ:

   ```csharp
   using System;
   using System.Collections;

   // Lớp tập hợp chứa các phần tử
   class MyCollection : IEnumerable
   {
       private int[] items;

       public MyCollection()
       {
           items = new int[5] { 1, 2, 3, 4, 5 };
       }

       // Triển khai phương thức GetEnumerator() của IEnumerable
       public IEnumerator GetEnumerator()
       {
           return new MyIterator(items);
       }
   }

   // Lớp duyệt qua các phần tử trong tập hợp
   class MyIterator : IEnumerator
   {
       private int[] items;
       private int currentIndex;

       public MyIterator(int[] collection)
       {
           items = collection;
           currentIndex = -1;
       }

       // Triển khai phương thức MoveNext() của IEnumerator
       public bool MoveNext()
       {
           currentIndex++;
           return (currentIndex < items.Length);
       }

       // Triển khai thuộc tính Current của IEnumerator
       public object Current
       {
           get { return items[currentIndex]; }
       }

       // Triển khai phương thức Reset() của IEnumerator
       public void Reset()
       {
           currentIndex = -1;
       }
   }

   // Sử dụng Iterator Design Pattern
   class Program
   {
       static void Main(string[] args)
       {
           MyCollection collection = new MyCollection();

           foreach (var item in collection)
           {
               Console.WriteLine(item);
           }
       }
   }
   ```

   Kết quả:
   ```
   1
   2
   3
   4
   5
   ```

2. Triển khai Iterator Design Pattern bằng `yield`:
   - `yield` là một từ khóa trong C# cho phép tạo một iterator mà không cần triển khai các phương thức `IEnumerator`.
   - Một phương thức chứa từ khóa `yield` trả về một `IEnumerable` hoặc `IEnumerator` và được gọi như một iterator khi được duyệt qua.

   Ví dụ:

   ```csharp
   using System;
   using System.Collections;

   class MyCollection
   {
       private int[] items;

       public MyCollection()
       {
          

 items = new int[5] { 1, 2, 3, 4, 5 };
       }

       // Sử dụng từ khóa yield để triển khai iterator
       public IEnumerable GetIterator()
       {
           foreach (var item in items)
           {
               yield return item;
           }
       }
   }

   // Sử dụng Iterator Design Pattern
   class Program
   {
       static void Main(string[] args)
       {
           MyCollection collection = new MyCollection();

           foreach (var item in collection.GetIterator())
           {
               Console.WriteLine(item);
           }
       }
   }
   ```

   Kết quả tương tự như trên.

Iterator Design Pattern cho phép duyệt qua các phần tử trong một tập hợp mà không cần biết cấu trúc nội bộ của tập hợp đó. Điều này giúp tách biệt việc duyệt qua các phần tử khỏi việc xử lý logic trong tập hợp, làm cho mã nguồn linh hoạt và dễ bảo trì.
