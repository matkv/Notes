# C#

Most of these notes are my personal notes I'm taking while going through the book [C# in Depth](https://csharpindepth.com/).

# Evolution of C#

Here are some of the most important themes of C# evolution and a brief examples of them

## Type system, concise code, LINQ, asynchrony, efficiency & C# versions

### Generics

In C# 1, we might have used code like this:

```csharp
public class Bookshelf
{
    public IEnumerable Books {get {...}}
}
```

With **generics**, introduced in C#2, we can specify the type of the IEnumerable and communicate more effectively:

```csharp
public class Bookshelf
{
    public IEnumerable<Book> Books {get {...}}
}
```

### Nullable reference types

C#2 also brought **nullable value types**, allowing the absence of information to be expressed effectively. C#7 made it possible to tell the compiler that a user-defined struct should be immutable using ```readonly struct``` declarations.

The plans for C#8 include **nullable reference types**. Right now, nothing in the language lets us express whether a reference (return value, parameter, local variable) might be null. C#8 will expect that anything not explicitly nullable is intended not to be nullable:

```csharp
string Method(string x, string? y)
```

This means x shouldn't be ```null```, y may be ```null``` and the method won't return ```null```.

### Anonymous types and implicitly typed local variables (var)

These help address the downside of some statically typed languages: verbosity. Sometimes we don't necessarily need to create a extra type for a partical data shape within a single method.

```csharp
var book = new {Title = "The Road", Author = "Cormac McCarthy"};

string title = book.Title;
string author = book.Author;
```

It is also not necessary to explicitly specify the type of a variable that is initialized in the same statement with the constructor.

```csharp
Dictionary<string, string> map1 = new Dictionary<string, string>();

//cleaner version

var map2 = new Dictionary<string, string>();
```

The second variable is still statically typed (not dynamically), but we didn't have to write the type explicitly. We can't use anonymous types as method parameters or return types.

#### Tuples instead of anonymous types

Instead of using the preceeding anonymous type, we could use the following:

```csharp
var book = {title: "The Road", author: "Cormac McCarthy"};

Console.WriteLine(book.Title);
```

A benefit of using tuples is that the **can** be used as method parameters and return types.

### Concise code

C#'s new features allow us to remove ***boilerplate code*** - redundant code that was distracting and unnecessary.

#### Construction and initialization

Lambda expression to subscribe a new event handler to a button's click event:

```csharp
button.Click += (sender, args) => MessageBox.Show("Clicked"!);
```

Object and collection initializers introduced in C#3 let us quickly initialize an object and set properties during initialisation:

```csharp
var order = new Order
{
    OrderID = "xyz",
    Customer = new Customer{ Name = "Jon", Address = "UK"},
    Items =
    {   
        new OrderItem { ItemId = "abcd123", Quantity = 1 },
        new OrderItem { ItemId = "fghi456", Quantity = 2 }
    }
}
```

#### Method and property declarations

**Automatically implemented properties** allows us to go from this:

```csharp
private string name;
public string Name
{
    get { return name; }
    set { name = value; }
}
```

To This:

```csharp
public string Name {get; set;}
```

#### Expression-bodied members

They also remove boilerplate code. Let's say we have a class with the members ```Count``` and ```GetEnumerator``` and we have a list (a collection of strings for example) and we want to delegate the ```Count``` and ```GetEnumerator()``` members of our class to that collection.

Instead of having to do this:

```csharp
public int Count {get {return list.Count;} }

public Ienumerator<string> GetEnumerator()
{
  return list.GetEnumerator();
}
```

We can remove a lot of the unnecessary code and use this shorter version:

```csharp
public int Count => list.Count;

public IEnumerator<string> GetEnumerator() => list.GetEnumerator();
```

#### String handling

* Information attributes -> ability for compiler to automatically populate method and filenames as parameter values.
* ```nameof``` -> allows names of variables, types, methods and other members to be represented in a refactoring-friendly form.
* Interpolated string literals -> value of a variable or property can be used directly instead of having to use string.Format{}

Interpolated string literals example:

```csharp
throw new KeyNotFoundException($"No calendar system for ID {id} exists");
```

#### Simple data access with LINQ

LINQ lets us use SQL-like queries in our code while still having compile-time checking and IntelliSense support. We can use that same syntax for regular collections as well via **expression trees**. These represent code as data, and LINQ can analize the code to convert it into SQL or other query languages.

```csharp
var offers =
  from product in db.Products
  where product.SalePrice <= product.Price / 2
  orderby product.SalePrice
  select new {
    product.Id, product.Description,
    product.SalePrice, product.Price
  };
```

#### Asynchrony

The ```async/await``` feature consists of two complementary parts around async methods:

* Async methods produce a result representing an asynchronous operation - this is usually ```Task``` or ```Task<T>```
* Async methods use await expressions to consume asynchronous operations. If the method tries to await an operation that **hasn't finished yet**, the method **pauses asynchronously** until the operation completes and then continues.

An example:

```csharp
private async Task UpdateStatus()
{
  // this starts two operations concurrently (side by side)
  Task<Weather> weatherTask = GetWeatherAsync();
  Task<EmailStatus> emailTask = GetEmailStatusAsync();
  
  // this asynchrounously waits for them to complete
  Weather weather = await weatherTask;
  EmailStatus email = await emailTask;
  
  // update GUI
  weatherLabel.Text = weather.Description;
  inboxLabel.Text = email.InboxCount.ToString();  
}
```

Async/await is aware of synchronization contexts. In that example, we're updating the user interface, which can be done only in a UI thread, despite also starting and waiting for long running operations. 

It takes away a lot of the boilerplate code that was previously required to achieve asynchrony.

#### Efficiency vs. complexity

C# 7 was the most performance-sensitive release: ```Read-only structs``` & ```ref``` features helped to avoid redundant copying. The ```Span<T>``` reduces unnecessary allocation and garbage collection.

#### Minor C# versions

The C# compiler defaults to using the earliest minor version of the latest major version it supports. If we want to use a later minor version, we have to specify that manually (in the project file or the project properties in Visual Studio).

This doesn't change the version of the compiler we run, it changes the set of language features available to you.

### C# as an evolving platform

For many years, running C# code would almost always mean running on Windows - either a client-side app written in WinForms or WPF or a server-side app written with ASP.NET and running behind Internet Information Server (IIS). The **Mono** project allowed C# projects to run on Linux, but most of the .NET development was still on Windows.

With the development of **.NET Core** - a runtime and framework that is portable and open source that is fully supported by Microsoft on multiple operating systems - this changed. Added to that there is a portable and open source IDE in the form of Visual Studio code.

Another way C# runs these days is **Xamarin** which provides a rich multiplatform mobile experience. With its GUI framework Xamarin Forms it allows developers to create user interfaces that are fairly uniform across different devices but can take advantage of the underlying platform.

**Unity** is one of the most popular game-development platforms in the world. But with its customized Mono runtime and ahead-of-time compilation, it can provide challenges to C# developers who are used to more-traditional runtime environments.

**Try .NET** allows users to try C# code in a browser with autocompletion and running the code. **Blazor** is a platform for running Razor pages directly in a browser.

#### Community

In 2010, the **NuGet** package manager was launched, which made it much easier to produce and consume class libraries, whether commercial or open source.

Under the umbrella of the .NET Foundation, .NET Core was announced. .Net Core, ASP.NET Core, Entity Framework Core and Visual Studio Code were all open source on GitHub - which increased third-party open source packages. It is now possible to for example run an ASP.NET Core service in a Docker image and deploy it with Kubernetes.