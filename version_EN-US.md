## Questions

1. [Copy vs Readonly](#copy-vs-readonly)
2. [Copy vs Strong](#copy-vs-strong)
3. [Weak vs Strong](#weak-vs-strong)
4. [Weak vs Unowned](#weak-vs-unowned)
5. [Gist of all the attributes](#gist-of-all-the-attributes)
6. [ARC & Retain Cycle](#arc-and-retain-cycle) 
7. [Optional in Swift](#optional-in-swift)
8. [What is ??](#what-is-??)
9. [Optional Chaining](#optional-chaining)
10. [Optional Binding](#optional-binding)
11. [Delegate vs Notification](#delegate-vs-notification)
12. [Class vs Struct](#class-vs-struct)
13. [Enum](#enum)
14. [Guard](#guard)
15. [Defer](#defer)
16. [MVVM](#mvvm)
17. [Dynamic Dispatch](#dynamic-dispatch)
18. [Static Dispatch](#static-dispatch)
19. [Closure](#closure)
20. [@escaping & nonescaping](#@escaping-and-nonescaping)
21. [What is "lazy"?](#what-is-lazy?)
22. [Unowned self & weak self](#unowned-self-&-weak-self)
23. [Process & Threads](#process-&-threads)
24. [Operation & GCD](#operation-&-GCD)
25. [Operation](#operation)
26. [OperationQueue](#operationQueue)
27. [GCD - Grand Center Dispatch](#GCD-grand-center-dispatch)
28. [What does a Dispatchgroup do?](#what-does-a-dispatchgroup-do?)
29. [Codable & Decodable in Swift](#codable-&-decodable-in-swift)
30. [Codable for complex JSON](#codable-for-complex-JSON)

## Copy vs Readonly

- Copy

It creates new copy of an object, and once new object is created retain count will be 1
Use copy when you need the value of an object as it is, and you don’t want other object to update the value of your object

- Readonly

Indicates that the property is readonly
Only generates getter, no setters will be generated
If you try to change value, you will get compiler error

# Copy vs Strong

- Copy

It creates new copy of an object, and once new object is created retain count will be 1
Use copy when you need the value of an object as it is, and you don’t want other object to update the value of your object
Create setters e getters 

- Strong

Increases the retain count by 1
Creates setters and getters
Object will be mutable

# Weak vs Strong

- Weak

Does not increase the retain count
Don’t protect the object from being deallocated by ARC
On deallocation, weak objects will be set to nil, and that’s all weak references are optional
Creates setters and getters

- Strong

Increases the retain count by 1
Protects the object from being deallocated by ARC
Creates setters and getters
Object will be mutable

# Weak vs Unonwned

- Weak

Does not increase the retain count
Don’t protect the object from being deallocated by ARC
On deallocation, weak objects will be set to nil, and that’s all weak references are optional
Creates setters and getters

- Unowned

Does not increase the retain count
On deallocation, weak objects will be set to nil, and that’s why all weak references are optional
Creates setters and getters

Note: It’s important that you only use unowned references when you really know that the object will never be nil once it has been set

# Gist of all the attributes

- Strong: Add reference to keep the object alive;
- Weak: doesn’t add reference so object can become nil by arc
- Assign: normal assign, no reference, used mostly for primitive data types
- Copy: makes new copy of an object, the copy will be immutable
- Nonatomic: makes not thread safe objects, increases perfomance
- Readwrite: Creates the getter & setters
- Readonly: Creates only getters

# ARC & Retain Cycle

ARC is apples way of handling memory management for us. What is does is, for each object it keeps a count of how many strong references are pointing to that object. And as long as there is a strong reference for a object, the object will stay in memory.

# Optional in Swift

Optional allows you to write flexible and more safe code;
Question mark means, it can be nil or some value

# What is ??

To provide default value for a variable which can be nil
It says hey if its nothing there then use this value
It is similar to saying “!=nil”

# Optional Chaining

Optional chaining is the way by which we try to retrieve a values from a chain of optional values
Allows you to fail gracefully when you try to access a property of an object which is nil

ex: `let album = albumReleased(year: 2006)?.uppercased()`

Optional chaining can be as long as required

# Optional Binding

Other than forced unwrapping, optional binding is a simpler and recommended way to unwrap an optional. You use optional binding to check if the optional contains a value or not. If it does contain a value, unwrap it and put it into a temporary constant or variable; With optional binding, you are creating a new reference to whatever you just unwrapped, and generally, that’s strong reference.

ex: 

```
if let constantName = someOptional {
   statements
}
```

# Delegate vs Notification

Delegates: used in one to one communication
Notification: used in one to many communication

# Class vs Struct

Class: reference type, means any changes in one ref, will effect other ref as well
Struct: value type, means changes in one value will not effect the others

ex:

```
class SomeClass {
	var name: String
		init(name: String) {
			self.name = name
		}
}

Var aClass = SomeClass(name: “”Bob)
Var bClass = aClass // aClass and bClass now reference the same instance!
bClass.name = “Sue”
print(aClass.name) //“Sue” print(bClass.name) //“Sue”
```

```
struct SomeStruct {
	var name: string
		init(name: String) {
			self.name = name
		}
}

var aStruct = SomeStruct(name: “Bob”)
var bStruct = aStruct // aStruct and bStruct now reference the same instance
bStruct.name = “Sue” 
print(aStruct.name) // “Bob”
print(bStruct.name) // “Sue”
```

# Enum

Group of related values

Raw = values defined in Enum

```
Enum Directions: Int {
  case up = 1
	case down
	case left	
  case right
}
```

Associated = passed as param to a enum

```
Enum ExampleAssociation {
	case name(String)
}
```

# Guard

Provides early exit, and doesn’t allow any code if condition is not true

# DEFER

Defer statement is used to execute a piece of code exactly before the execution departs the recent scope;
The defer statement is executed after the return!
The defer statement is executed no matter how you exit

```
Func deferEx() {	
  print(“”beginning)	
  var value: String?	
  defer {		
    if let v = value {			
      print(“Ending execution of \(v)”)		
      }	
    }
	value = “defer function”	
  print(“Ending”)
}
```

# MVVM

In MVC - View send events to the Controller, the controller then send request to model for data and perform business logic if required, model notifies controller in case of any data change and controller send data to View to presentMVC - Resulted into massive view controller which were difficult to manage
In MVVM - View Controller and View is combined to become “View”And one more layer is added called “ViewModel”, this new layer will communicate with model and process the data and perform some business logic if required and sends final data to ViewController that is only required to update the UI.

# Dynamic Dispatch

Dynamic dispatch is the process of selecting which implementation of a polymorphic operation (method or function) to call at run time;
For example, if a subclass overrides a method of its superclass, dynamic dispatch figures out which implementation of the method needs to be invoked, that of the subclass or that of the parent class;
By applying the “dynamic” declaration modifier to a member of a class, you tell the compiler that dynamic dispatch should be used to access that member;
“Dynamic” declaration modifier can only be used for members of a class. Structures and enumerations don’t support inheritance, which means the runtime doesn’t have to figure out which implementation it needs to use;Swift provides 2 ways to achieve dynamism: Table Dispatch and Message Dispatch;
Table Dispatch: With this method, a class is associated with a so-called virtual table which comprises an array of function pointers to the real implementation corresponding to that class. Note that the table is constructed at compile time. Thus, there are only two additional instructions (read and jump) as compared to static dispatch. So the dispatch should be theoretically pretty fast.

Message Dispatch: It is objective-c that provides this mechanism. Every time an Objective-C method is called, the invocation is passed to “objc_msgSend” which handles the look ups. Unlike table dispatch, the message passing dictionary could be modified at runtime, enabling us to adjust the program behaviors while running.

# Static Dispatch

When something is statically dispatched, we are dealing with the opposite scenario. With static dispatch, the compiler does in fact know which property or method is being called at runtime, which is a performance boost. You can achieve static dispatch by marking a base class with the “final” keyword. This lets the compiler know that this class can not have any subclasses and that the method/property you are referring to is its only implementation.

Another example is the “static“ keyword for when defining type methods of properties. This keyword is really just short for “final class”. This lets the compiler know that this is the final implementation of this method and it will not be overridden. Therefore, it will be statically dispatched.When defining a type method you can mark it with “class” or “static”, but which you choose determine how it will be dispatched. 


# Closure

Closures are self-contained blocks of functionality that can be passed around and used in your code;
Closures are headless functions. Closures are functions without the func keyword and the function name. They are also known as anonymous functions.

Syntax -
```
{ (parameter) -> return type in
	statement 
}
```

ex:
```
var sayHello = {(name: String) -> String in
	return “Hello \(name)” 
}
sayHello(“Richa”)

Passing inside a function syntax -

Func sayHello(name: string, closure(String) -> void) {
	closure(“Hello \(name)”)
}
sayHello(name: “Richa”) { name in 
	print(name)
}
```

# @escaping & @nonescaping

If a closure is passed as an argument to a function and it is invoked after the function returns, the closure is escaping;
Its mostly useful/required for network calls, you would want your completion handler to live after return statement;
There are many different benefits of making non-escaping, it will take care about the memory allocation for the closure

# What is “lazy”?

A lazy stored property is a property whose initial value is not calculated until the first time it is used. You indicate a lazy stored property by writing the “lazy” modifier before its declaration. If the your app is a complex one, then the memory issues are one of the major challenges. So, the developer should be really writing an optimized code which consider memory allocation at first place. The developer need to avoid doing expensive work unless it’s really needed. We can achieve that by using lazy;

You can’t use lazy with let;
Your can’t use it with computed properties. Because, a computed property returns the value every time we try to access it after executing the code inside the computation block;
You can use lazy only with members of struct and class;
Lazy variables are not initialized automatically and so is not thread safe

# [unowned self] & [weak self]

The only time where you really want to use [unowned self] or [weak self] is when you could create a strong reference cycle. A strong reference cycle is when there is a loop of ownership where objects end up owning each other (maybe through a third party) and therefore they will never be deallocated because they are both ensuring that each other stick around;

In case of a closure, you just need to realize that any variable that is referenced inside of it, gets “owned” by the closure. As long as the closure is around, those objects are guaranteed to be around. The only way to stop that ownership, is to use the [unowned self] or [weak self]. So if a class owns a closure, and that closure captures a strong reference to that class, then you have a strong reference cycle between the closure and the class. This also includes if the class owns something that owns the closure;

If self could be nil in the closure use [weak self];
If self will never be nil in the closure use [unowned self]

# Process & Threads

A process can contain multiple threads of execution, and each thread can perform multiple tasks one at a time;
Task: A simple, single piece of work that needs to be done;
Thread: A mechanism provide by the operating system that allows multiple sets of instructions to operate at the same time within a single application;
Process: An executable chunk of code, which can be made up of multiple threads

# Operation & GCD

Both are used to do any type of multithreading operation in iOS
GCD: Is a lightweight way to represent units of work that are going to be executed concurrently. You don’t schedule these units of work; The system takes care of scheduling for you. Adding dependency among blocks can be a headache. Cancelling or suspending a block creates extra work for you as a developer! Operation: Adds a little extra overhead compared to GCD, but you can add dependency among various operations and re-use, cancel or suspend them.

Operation and OperationQueue are built on top of GCD. As a very general rule, apple recommends using the highest-level abstraction, then dropping down to lower levels when measurements show this is necessary.


# Operation

Operation is an abstract class, designed for sub-classing. Each subclass represents a specific task.
Main() is the method you override in Operation subclasses to actually perform work.

```
Class imageDownloader: Operation {
	let photoRecord: PhotoRecord
	init (_ photoRecord: PhotoRecord) {
		self.photoRecord = photoRecord	
	}
	override func main() {
		guard let imageData = try? Data(contentsOf: photoRecord.url) else { return }
		if !imageData.isEmpty {
			photoRecord.image = UIImage(data: imageData)
		}
	}
}
```

# OperationQueue

A queue that regulates the execution of operations
An operation queue executes its queued Operation objects based on they priority and readiness. After being added to an operation queue, an operation remains in its queue until it reports that it is finished with its task;OperationQueue is particularly powerful because it lets you control precisely how many simultaneous operations can run and what quality of service you need, while also letting you schedule work using closures. You can even ask the operation queue to wait until all its operations are finished, which makes scheduling easier.

```
let queue = OperationQueue()
	for image in images {
		queue.addOperation {
			self.process(image)
		}
	}
queue.waitUntiAllOperationsAreFinished()
```

You can add as many operations as you want, but they don’t all get executed at the same time. Instead, OperationQueue limits the number of operations based on system conditions - if it’s a more powerful device that isn’t doing much right now, you’ll get more operations than a less powerful device or a device that’s busy with other work.

# GCD - Grand Center Dispatch

Is a low-level API for managing concurrent operations
DispatchQueue - 
- Global Queue: Using to perform non-UI work in the background
- Main Queue: Using to update the UI after completing work in a task on a concurrent queue

List of priority: 
- .userInteractive 
- .userInitiated 
- .default 
- .utility 
- .background 
- .unspecified

```
DispatchQueue.global(cos: .background).async {
	// Call your background task
	DispatchQueue.main.async {
		// UI updates here for task complete.
	}
}
```

# What does a DispatchGroupd do?

Let’s say you’ve got several long running tasks to perform. After all of them have finished you’d like to run some further logic. You could run each task in a sequential fashion, but that isn’t so efficient - you’d really like the former tasks to run concurrently. DispatchGroup enables you to do exactly this.

Ex: You need to run two distinct network calls. Only after they’ve both returned do you have the necessary data to parse the responses.
An animation is running, parallel to a long database call. Once both of those have finished, you’d like to hide a loading spinner.


# Codable & Decodable in Swift

Make your data types encodable and decodable for compatibility with external representations such as JSON.
Codadle protocol is new protocol introduced by Apple in Swift 4 can provide Encodable and Decodable built-in feature. It will make JSON parsing easier.

```
Struct User: Codable {
	var userId: Int
	var id: Int
	var title: String
	var completed: Bool
}
do {
	let decoder = JSONDecoder()
	let model = try decoder.decode([User].self, from: dataResponse)
	print(model)
} catch let parsingError {
	print(“Error”, parsingError)
}
```

# Codable for complex JSON

```
Let jsonDataString = “” {
    	“status”: “success”,	
        “statusCode”: 123,	
        “document”: {		
            “count”: 1,		
            “profiles”: [{
                “name”: “Luísa”,
                “email”: “luisa@gmail.com”
		}]
	}
}“”.data(using: .utf8)!

struct Response: Codable {
	let status: String?	let statusCode: Int?	let document: Document?
}struct Document: Codable {
	let count: Int?	let profiles: [Profiles]?}

struct Profiles: Codable {
	let name: String?
	let email: String?	
}
do {
	let response = try JSONDecoder().decode(Response.self, from: jsonData)	print(response)
} catch {	
    print(error)
}
```
