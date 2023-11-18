# C Sharp Notes

## Keywords

    abstract: Used to declare an abstract class or an abstract method within an abstract class.
    as: Used for type conversion without raising an exception if the conversion fails.
    base: Used to access members of the base class from within a derived class.
    bool: Declares a variable to hold a Boolean value (true or false).
    break: Terminates the closest enclosing loop or switch statement.
    byte: Declares a variable to hold an 8-bit unsigned integer.
    case: A switch statement label.
    catch: Used to define a block of code to handle exceptions.
    char: Declares a variable to hold a Unicode character.
    class: Used to declare a class.
    const: Declares a constant value.
    continue: Skips the current iteration of a loop and moves to the next iteration.
    decimal: Declares a variable for a high-precision decimal number.
    default: Can specify the default value of a type or the default case in a switch statement.
    delegate: Declares a delegate type.
    do: Used in the do-while loop.
    double: Declares a variable to hold a double-precision floating point number.
    else: Used in conditional statements (if-else).
    enum: Used to declare an enumeration, a distinct type consisting of a set of named constants.
    event: Declares an event.
    explicit: Defines a user-defined type conversion operator that must be invoked with a cast.
    extern: Used to declare a method that is implemented externally.
    false: Represents the boolean value false.
    finally: Defines a block of code, used with exceptions, that is executed regardless of whether an exception is thrown.
    fixed: Prevents the garbage collector from relocating a movable variable.
    float: Declares a variable to hold a single-precision floating point number.
    for: Defines a for loop.
    foreach: Defines a loop that iterates through a collection.
    goto: Provides an unconditional jump to a labeled statement.
    if: Used to test a condition.
    implicit: Defines an implicit user-defined type conversion operator.
    in: Used in a foreach loop to indicate the collection being iterated.
    int: Declares a variable to hold a 32-bit signed integer.
    interface: Used to declare an interface.
    internal: Specifies that access is limited to the current assembly.
    is: Checks if an object is compatible with a given type.
    lock: Used to ensure that a block of code runs only in a single thread at a time.
    long: Declares a variable to hold a 64-bit signed integer.
    namespace: Used to declare a scope that contains a set of related objects.
    new: Used to create objects or hide inherited members.
    null: Represents a null reference.
    object: Declares a variable that can hold any type of data.
    operator: Used to define/overload an operator.
    out: Indicates that a parameter is passed by reference and is intended to be modified by the called method.
    override: Indicates that a virtual method is overridden in a derived class.
    params: Allows a method to accept a variable number of arguments.
    private: Specifies that access is limited to the containing type.
    protected: Specifies that access is limited to the containing class or types derived from the containing class.
    public: Specifies that there are no restrictions on accessing the member.
    readonly: Declares a field that can only be assigned a value during declaration or in a constructor in the same class.
    ref: Indicates that a parameter is passed by reference.
    return: Exits a method and optionally returns a value.
    sbyte: Declares a variable to hold an 8-bit signed integer.
    sealed: Specifies that a class cannot be inherited or that a method cannot be overridden.
    short: Declares a variable to hold a 16-bit signed integer.
    sizeof: Returns the size in bytes of the unmanaged type.
    stackalloc: Allocates a block of memory on the stack.
    static: Indicates that a member belongs to the type itself rather than to any specific object.
    string: Declares a variable to hold a sequence of characters.
    struct: Declares a value type that

## Classes

    public:
        Use public when you want the class or its members to be accessible from any other code in the same assembly or another assembly that references it.
        Example: public class MyClass { ... }
        This is commonly used for classes that form the public API of a library or framework.

    private:
        private is used when you want the members of a class to be accessible only within the same class.
        Example: private int myPrivateField;
        This is the default access level for class members. It's used to encapsulate the internal state of the class.

    protected:
        Use protected for class members you want to make accessible only within the class itself and by derived classes.
        Example: protected void MyProtectedMethod() { ... }
        This is ideal for methods and properties that should be available to child classes but not to the rest of the application.

    internal:
        internal classes or members are accessible within the same assembly, but not from other assemblies.
        Example: internal class MyInternalClass { ... }
        This is useful for internal workings of a framework or library where you want to limit access to the assembly.

    protected internal:
        This combination allows access to the class or its members within the same assembly or in derived classes in other assemblies.
        Example: protected internal int MyVar;
        It’s less commonly used but can be helpful in specific scenarios where you need a wider access range than protected but more restricted than public.

    private protected:
        This combination limits access to the containing class or types derived from the containing class within the current assembly.
        Example: private protected int MyVar;
        It's useful when you want to allow access to derived classes but only within the same assembly.

    No Modifier (Default for classes):
        When no access modifier is specified for a class, it defaults to internal.
        Example: class MyClass { ... }
        This means the class is accessible within the same assembly but not from outside.

### Class Examples

public:

    Scenario: Creating a library where certain classes need to be accessed by other applications.
    Example:

```csharp

public class Logger {
    public void LogMessage(string message) { ... }
}
```

In this scenario, the Logger class and its LogMessage method are accessible to any other class in any assembly that references this library.

private:

    Scenario: Defining internal implementation details of a class that should not be exposed outside the class.
    Example:

```csharp

public class Account {
    private double balance;

    public void Deposit(double amount) {
        balance += amount;
    }
}
```

Here, balance is a private field of the Account class, only accessible within the Account class itself.

protected:

    Scenario: Allowing derived classes to access certain properties or methods, while keeping them hidden from other classes.
    Example:

```csharp

public class BaseClass {
    protected int Id { get; set; }
}

public class DerivedClass : BaseClass {
    public void DisplayId() {
        Console.WriteLine(Id);
    }
}
```

In this case, Id is accessible within BaseClass and DerivedClass, but not outside these classes.

internal:

    Scenario: Designing components in a large application that should only be used within the same assembly.
    Example:

```csharp

internal class InternalHelper {
    internal void HelpMethod() { ... }
}
```

InternalHelper and its method HelpMethod are accessible anywhere within the same assembly but not from other assemblies.

protected internal:

    Scenario: Providing access to certain members of a class both within the same assembly and in derived classes in other assemblies.
    Example:

```csharp

public class BaseClass {
    protected internal void SharedMethod() { ... }
}
```

SharedMethod can be accessed within BaseClass, its derived classes (even in different assemblies), and other classes in the same assembly.

private protected:

    Scenario: Restricting access to members of a class strictly to derived classes within the same assembly.
    Example:

```csharp

public class BaseClass {
    private protected int InternalId { get; set; }
}

public class DerivedClass : BaseClass {
    public void DisplayId() {
        Console.WriteLine(InternalId);
    }
}
```

InternalId can only be accessed within BaseClass and its derived classes, but only if they are in the same assembly.

Default (internal for classes):

    Scenario: Creating classes within a single assembly that should not be exposed to other assemblies.
    Example:

```csharp

class HelperClass {
    public void Assist() { ... }
}
```

A Note about private 

Private classes in C# are typically nested within another class and are used to organize code and encapsulate functionality that is only relevant to the containing class. Here's a scenario to illustrate the use of private classes:

Scenario: Suppose you are developing a network scanning tool in C#. You might have a public class NetworkScanner that performs the scanning operation. However, within this class, you might need a helper class to handle specific details like parsing network responses or managing scan sessions. This helper class should not be accessible or even visible to other parts of your application, as its functionality is tightly coupled with the NetworkScanner class.

Example:

```csharp

public class NetworkScanner {
    // ...

    private class ScanSessionManager {
        public void StartSession() { ... }
        public void EndSession() { ... }
        // Other methods related to managing a scan session
    }

    public void PerformScan() {
        ScanSessionManager sessionManager = new ScanSessionManager();
        sessionManager.StartSession();
        // Perform scanning logic
        sessionManager.EndSession();
    }

    // Other methods of NetworkScanner
}
```

In this example, ScanSessionManager is a private nested class within NetworkScanner. It's used for managing the lifecycle of a network scan session. The methods of ScanSessionManager (StartSession, EndSession, etc.) are accessible only within the NetworkScanner class and are not exposed to the outside world. This encapsulation ensures that the internal workings of the network scanning process are hidden, reducing the complexity of the public interface of the NetworkScanner class and preventing misuse or unintended interactions from other parts of the application.

HelperClass is accessible within the same assembly but not accessible to other assemblies.
