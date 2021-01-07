---
title: 'Swift_iOS_Basic'
date: 2020-12-19T17:18:05+01:00
draft: false
---





## If

```swift
if age < 20 {
    
} else if age > 20 {
    
} else {
    
}
```



## Ternary Operator

`a ? b : c`.   

Ternary operator reads something like, “If a is true, then do b. else do c



## String

```swift
let name = "abc"
print(name[0])  // error
```



Swift uses a type called `String.Index` to keep track of indices in string instances. (The period in String.Index just means that Index is a type that is defined on String.

 To find the character at a particular index, you begin with the String type’s `startIndex` property. This property yields the starting index of a string as a String.Index. You then use this starting point in conjunction with the `index(_:offsetBy:)` method to move forward until you arrive at the position of your choosing.



```swift
let start = playground.startIndex                          String.Index
let end = playground.index(start, offsetBy: 4)             String.Index
let fifthCharacter = playground[end]                       "o"

```



```swift
let range = start...end                                    {{_rawBits 1}, {_rawBit...
let firstFive = playground[range]                          "Hello"
```



| Access level           | Description                                                  | Visible to…                           | Subclassable within…                  |
| :--------------------- | :----------------------------------------------------------- | :------------------------------------ | :------------------------------------ |
| open                   | Entities are visible and subclassable to all files in the module and those that import the module. | defining module and importing modules | defining module and importing modules |
| public                 | Entities are visible to all files in the module and those that import the module. | defining module and importing modules | defining module                       |
| internal (the default) | Entities are visible to all files in the same module.        | defining module                       | defining module                       |
| fileprivate            | Entities are visible only within their defining source file. | defining file                         | defining file                         |
| private                | Entities are visible only within their defining scope.       | scope                                 | scope                                 |



## Memory Management

All of the objects and values that your app uses take up memory. When those objects and values are no longer needed, you want the system to reclaim that memory it so that it can be reused.

Memory management in Cocoa is relatively simple. For instances of value types, there is nothing to worry about. The memory is immediately reclaimed as soon as the variable goes out of scope or when the reference type that it is part of (e.g., a property is a part of an object) is itself reclaimed.

As reference types, objects are much more interesting because their lifetimes are not tied to scope. Objects frequently live longer than the methods in which they are created. Cocoa uses reference counting to manage their lifetimes.

## Automatic Reference Counting

Reference counting addresses two needs:

- Your objects need to stay in memory as long as they are needed…
- … and no longer. Objects you no longer need should be deallocated as soon as possible.

Reference counting works through simple bookkeeping: As long as there is a reference to an object, the object will be kept in memory. When there are no more references, the object is deallocated. The good news is that in these modern times you do not have to do this bookkeeping yourself: you have ARC, or Automatic Reference Counting, to do it for you. Before you learn how ARC works, you should understand references and reference counts.

### OBJECTS HAVE REFERENCE COUNTS

When an object is created, there is always an initial reference to it – the property, outlet, constant, or variable that stores the result of creating the object. This gives the brand-new object a reference count of 1. Whenever that reference is assigned or passed elsewhere, another reference is created and the object’s reference count is incremented.

When the value of a property, outlet, or variable changes to reference another object or to be nil, then the previously referenced object has “lost a reference,” and its reference count is decremented.

An object also loses a reference when the referring property, outlet, constant, or variable is itself destroyed. For local constants and variables, this happens when the constant or variable goes out of scope. For properties and outlets, this happens when the instance that declares the property or outlet is deallocated. 

Let’s look at an example from RandomPassword’s AppDelegate.swift. At the beginning of applicationDidFinishLaunching(_:), you create an instance of MainWindowController and assign it to the mainWindowController local constant. This creates a reference to the new MainWindowController, which has a reference count of 1.

```swift
    func applicationDidFinishLaunching(aNotification: NSNotification) {
        // Create a window controller
        let mainWindowController = MainWindowController()
        ...
    }
```



At the end of the same method, AppDelegate’s mainWindowController property is assigned to reference the same instance of MainWindowController. Setting the property creates another reference, so the MainWindowController instance now has a reference count of 2.



```swift
    func applicationDidFinishLaunching(aNotification: NSNotification) {
        // Create a window controller
        let mainWindowController = MainWindowController()
        // Put the window of the window controller on screen
        mainWindowController.showWindow(self)
        // Set the property to the window controller
        self.mainWindowController = mainWindowController
    }
```



When applicationDidFinishLaunching(_:) returns, the local constant goes out of scope, and the MainWindowController loses a reference. However, the MainWindowController will not be deallocated because another reference – the property – continues to exist.

### DEALLOCATING OBJECTS IN A HIERARCHY

[Figure 4.1](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch04.html#fig-ARCDiagram1) shows the objects that make up RandomPassword’s interface.



**Figure 4.1 Chain of references in view hierarchy**

![Chain of references in view hierarchy](../../themes/hello-friend/images/TreeNodeReferenceCycle.png)

Let’s walk through the references in this diagram. You already know that the MainWindowController’s reference count is 1 after the application has finished launching. The MainWindowController has a window property that has been set to an instance of NSWindow. This gives the window a reference count of 1 as well. The window has a contentView property set to an NSView, which also has a reference count of 1. 

The NSView has an array named subviews. Here is its property declaration:

```swift
    var subviews: [AnyObject]
```



Array<T> is not a reference type, but when an array’s members are instances of a reference type, then the array contains references, not instances. Thus, the NSView indirectly has references to the text field and the button.

Now think back to the references created to the MainWindowController in applicationDidFinishLaunching(_:). If you did not set the mainWindowController property to reference the MainWindowController, then that object would be deallocated. What would happen to the rest of the objects in the view hierarchy?

To find out, open the RandomPassword project and comment out the line in AppDelegate.swiftwhere the property is set.

```swift
    func applicationDidFinishLaunching(aNotification: NSNotification) {
        ...
        // Set the property to the window controller
        self.mainWindowController = mainWindowController
        // self.mainWindowController = mainWindowController
    }
```



Add a couple of println() statements to investigate what is happening. First, confirm that the window controller’s NIB file was loaded. In MainWindowController.swift, add a println() statement to the windowDidLoad() method. 

```swift
    @IBOutlet weak var textField: NSTextField!

    override func windowDidLoad() {
        super.windowDidLoad()
        println("window loaded from NIB named \(windowNibName)")
    }
```

Then, add an implementation of deinit() to MainWindowController. The deinitializer is called automatically when an instance is about to be deallocated.

```swift
    deinit {
        println("\(self) will be deallocated")
    }
```

Run the app. The app builds fine, but no window is visible. The console confirms that the NIB was loaded and then reports the immediate deallocation of the window controller:

```swift
    window loaded from NIB named MainWindowController
    <RandomPassword.MainWindowController: 0x6000000a1380> will be deallocated
```



What happened? The only reference to the MainWindowController was lost when applicationDidFinishLaunching(_:) returned and the mainWindowController constant went out of scope. Because the property was not set, losing this reference brought the window controller’s reference count to 0, and it was deallocated. 

But that is not all. When the window controller was deallocated, the reference to the window was lost. This reference was the only reference to the window, so the window was deallocated as well. With the window gone, the views in its hierarchy were deallocated in the same way.

This is a nice piece of clean-up. None of the view objects are left behind after the window was deallocated. View hierarchies are purposely set up this way to prevent parts of your interface from leaking after a higher-level view has been deallocated.

However, you want your window controller and its view hierarchy to stick around – at least for a while – after the application has launched. Restore the line that sets the mainWindowControllerproperty.

```swift
    func applicationDidFinishLaunching(aNotification: NSNotification) {
        ...
        // Set the property to the window controller
        // self.mainWindowController = mainWindowController
        self.mainWindowController = mainWindowController
    }
```

Run the app again to confirm that the window appears and that the console does not report the deallocation of the MainWindowController.





## Strong and Weak References

By default, a reference is a strong reference. All of the references you have seen so far have been strong references, and an object’s reference count is actually the count of strong references. As long as there is a strong reference to an object, that object will remain in memory.

There is another kind of reference: a weak reference. A weak reference allows you to access the object it references, but it is not included in the object’s reference count. Thus, a weak reference will not keep an object in memory.



In Swift, weak references are always optional types because they are auto-zeroing: when the referenced object is deallocated, the weak reference is set to nil. Auto-zeroing prevents references from dangerously storing an address of an object that no longer exists.

Try it out. Open MainWindowController.swift and change the mainWindowController property to a weak reference using the `weak` keyword:

```swift
    var windowController: MainWindowController?
    weak var windowController: MainWindowController?
```

Before you run the app: What do you think will happen?

The behavior is indistinguishable from not assigning the mainWindowController local variable to a property at all. Remove the `weak` keyword before continuing.

```swift
    weak var windowController: MainWindowController?
    var windowController: MainWindowController?
```

### STRONG REFERENCE CYCLES

There is one complicating factor in reference counting: when two objects have strong references to each other – either directly or indirectly – a strong reference cycle occurs. In a strong reference cycle, none of the objects can be deallocated because all of them have a non-zero reference count. The result is that a portion of the object graph is leaked – the memory will never be freed because all of the objects are keeping each other alive and there are no references to any of the objects. They are an island.

Why can’t ARC fix this problem? ARC is not garbage collection. Since ARC is part of the compiler it cannot analyze the references at runtime, so it is impossible for ARC to detect a strong reference cycle. Instead, you will have to spot the potential for a strong reference cycle and design your references to avoid it.

[Figure 4.2](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch04s02.html#fig-TreeNodeLeak) shows an example of a common strong reference cycle. The specific scenario is a tree, but it is representative of the more general scenario where there are parent-child relationships.



**Figure 4.2 A strong reference cycle**

![A strong reference cycle](../../themes/hello-friend/images/TreeNodeWeakReference.png)

Here is the code for Node, which causes the leak:

```swift
class Node {
    var children: [Node] = []
    var parent: Node?
}
```

In the diagram, MainWindowController has a strong reference, tree, to the root node. That node has one child, which has a strong reference back to its parent, the root. Therefore the root node has a reference count of 2, and its child has a reference count of 1.

When tree is set to `nil`, the root node’s reference count is decremented, bringing it to a reference count of 1. Because none of the objects’ reference counts have reached 0, nothing is deallocated, and the nodes are leaked.

The solution in this scenario is to make the parent reference a weak reference:

```swift
class Node {
    var children: [Node] = []
    weak var parent: Node?
}
```

[Figure 4.3](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch04s02.html#fig-TreeNodeWeak) shows the result. Because the parent reference is weak, the root node starts with a reference count of 1.



**Figure 4.3 Weak parent reference avoids the cycle**

![Weak parent reference avoids the cycle](../../../../../Desktop/typora_images/TreeNodeWeakReference.png)

When tree is set to nil, the root node’s reference count is decremented to 0, which deallocates the root node. Because the children array is a value type on the node, its strong references to the children are released, which causes the child’s reference count to reach 0, deallocating it. The entire tree of objects has been freed.

The key to avoiding strong reference cycles is to think in terms of “what owns what” in your object graph and make only those references strong. In a tree, the parent owns the children (strong reference); the child does not own the parent (weak reference).

Weak references are commonly used in three places in Cocoa:

-  Outlets to subviews: A window controller has a strong reference to the window, and a window has strong references (indirectly) to its view hierarchy. Therefore, a strong reference is unnecessary and could inadvertently keep a subtree of the view hierarchy alive.
-  Targets from controls: You will learn more about controls in [Chapter 5](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch05.html), but because a controller typically has indirect strong references to its controls, they should have weak references back to the controller where the action methods are implemented.
-  Delegates: Delegates will be covered in [Chapter 6](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch06.html), but the idea is the same as with controls and their targets.



### UNOWNED REFERENCES

Rarely, you may see references declared as unowned. An unowned reference is a non-strong, non-optional reference. Like a weak reference, it does not add to an object’s reference count. Unlike a weak reference, it is not set to nil when the referenced object is deallocated. 

What are unowned references for? For one thing, they have been used to make pre-ARC parts of the Cocoa frameworks compatible with ARC. Unowned references are also sometimes used in closures, which you will learn about in [Chapter 15](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch15.html).

In your code, an unowned reference is best used when you know that the reference will never be accessed after the referenced object has been deallocated. For example, you might have an one object whose lifetime is known to be a subset of the lifetime of the object that it is referencing.





## Delegation

You want to send data or message or some flag from child class to parent class

> If class A has reference to class B then class A is Parent and class B is its child.
>
> Delegate pattern works for class only..since its need reference



```swift
class A {
    var b = B()
    b.delegate = self   // you can also declare delegate as closure/ Notification/Publisher/Observable/Subject 
}

extension A: BDelegate {
    
}

```





## KVC, KVO, and Bindings

Key-value coding (KVC) is a mechanism that allows you to get and set the value of a property indirectly using a key

here we use property name as key

```swift
import Cocoa

class Student: NSObject{
    var name = ""
    var gardeLevel = 0
}
```



Student must be a class that inherits from NSObject (directly or indirectly) because the KVC methods that you will use shortly are defined on NSObject. 

Create an instance of Student and then use the KVC method setValue(_:forKey:) to update its properties.



```swift
let s = Student()                                       {__lldb_expr_...
s.setValue("Kelly", forKey:"name")                      {__lldb_expr_...
s.setValue(3, forKey:"gradeLevel")     
```



The KVC method for getting the value of a property with a key is valueForKey(_:). Use this method to access the same properties.



```swift
s.name                                                  "Kelly"
s.gradeLevel                                            3
s.valueForKey("name")                                   "Kelly"
s.valueForKey("gradeLevel")                             3
```



Why are these abilities interesting? By themselves, they may seem like just an interesting parlor trick, but many Cocoa features rely on the ability to get and set values by key. Let’s take a look at one of those features – Cocoa bindings.



## Completion Handlers and Closures

Completion handlers are a powerful mechanism for executing a block of code at the completion of a long-running operation. 

When function finished it call its closure at the end..due to this closure block defined by caller  will execute

Completion handlers inside a function == call the function defined outside by caller

> Use Result type for completion handler



## CLOSURES AND CAPTURING

Swift closures can capture constants and variables that are within scope. This means that you are not restricted by the parameters of the closure type: if a constant or variable is within scope, you can capture it and access it later when the closure is called.

This powerful feature has important implications for memory management. When an object reference is captured by a closure, a strong reference is made by default. This has the benefit of keeping the object in memory, but the disadvantage of potentially creating a strong reference cycle if the captured object reference has a strong reference to the closure, as demonstrated in [Figure 15.3](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch15s03.html#fig-Closures-StrongRefCycle-Diagram).



**Figure 15.3 Captured references in closures can create strong reference cycles**

![Captured references in closures can create strong reference cycles](../../../../../Desktop/typora_images/Closures.StrongRefCycle.Diagram-20210108000348794.png)



The solution to resolving a strong reference cycle from a closure is to use a capture list:

```swift
chauffeur.completionHandler = { [unowned chauffeur] in
    chauffeur.sendMessage("I have arrived at the portico.")
}
```



Capture lists allow you describe how reference types are captured. Two keywords come into play here: `unowned` and `weak`. If the reference being captured should never be deallocated before the closure, use `unowned`. This is similar to treating the capture as an implicitly unwrapped optional: accessing it will crash your application.

On the other hand, if the reference may be deallocated before the closure, use `weak`. This treats the capture as an optional. [Figure 15.4](https://learning.oreilly.com/library/view/cocoa-programming-for/9780134077130/ch15s03.html#fig-Closures-NoRefCycle-Diagram) shows how this hypothetical reference cycle was avoided.



**Figure 15.4 Strong reference cycle resolved using the capture list**

![Strong reference cycle resolved using the capture list](../../../../../Desktop/typora_images/Closures.NoRefCycle.Diagram-20210108000348796.png)



One last thing: if you reference any properties or methods on self, Swift requires you to use the selfconstant to make the fact that it will be captured clear. You can include self in the capture list if you need to.



Now that you have some background on closures, let’s put that knowledge to work.





## Creating and using custom subscripts

type subscript inside class/enum/struct/extension



```swift
class MyNames {
    private var names = ["Jon", "Kailey", "Kara"] 
    subscript(index: Int) -> String {
        get {
            return names[index]
        }
        set {
            names[index] = newValue
        }
    }
}
```



