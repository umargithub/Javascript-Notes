---
title: 'My First Post'
date: 2019-07-18T17:18:05+01:00
draft: false
hideReadMore: true
---

# 

# Protocol Oriented programming using Swift



In this tutorial, you will learn about Protocol and default implementaton of protocol using extension.



```swift
// For all type fo person in you app
class Person {
    // all Person of the world has these properties
    var name: String
    var age: Int
    init(name: String, age: Int){
        self.name = name
        self.age = age
    }
    // all person can Speak but some can't speak.. You may need to override if the person is mute... A sign of bas Design nut Still not to bad
    func speak(){
        print("I Can Speak")
    }
    .....
    .... 10,000 more codes well tested working fine.
}
```





// You received complaine from MutePersons.org  that this app does not

// respect mute person.. so you decide to subclass it and override it 

```swift

class MutePerson: Person {
    override func speak(){
        super.speak()
        print("I Can'\t speak")
    }
}
```



 Now imagine your app was using Person data type in whole apps thats was well tested and working well.

Since we also need to replace Some Persons with MutePerson. We need to modify aloat and we need to test again to make sure its working well.

This is consider as Bad Desgn due to class and inheritance.



If we have used Protocol design Pattern then all of above problems can be solved much easier. Lets assume we have used Protocol design first initially like



```swift
protocol Speak {
    func speak()
}

and our initial class was
like 

class Person: Speak {
    var name: String
    var age: Int
    init(name: String, age: Int){
        self.name = name
        self.age = age
    }
    
     func speak(){
       print("I Can Speak")
    }
}
```



// later Muteperson need to be added

```swift
class MutePerson: Speak {
    .....
    func speak(){
       print("I Can't Speak")  
        // no override no super no stronly connected..no unnecessay inheritance of data...
     //   No disturbance in well tested code
    }
}
```



// add special Offer to Mute Person after 1 years of introduction to MutePerson class

```swift
Protocol Offer {
    func getOffer()
}

// much easy to extend/ add new functionality due to Protocol
// Imagine if there was not protocol then we need to create another subclass to add a new functionality.
//Thats power of Protocol
extension MutePerson: Offer {
    func getOffer(){
        print("You received an offer")
    }
}
```



## First we need to know What's Protocol?

Protocol is a user defined data type like class and struct but unlike class and strcut Protocol has only declaraion of variables, methods and initializers.



## What are the Benefits of protocol over class or struct?

    Inheritance :- When you inherit from super class or general class

to make a specific class then both are decoupled (strongly connected)

and you need to inherit and use initializers / properties and methods of super class even you don;t want. If you want to provide another implementation then you need to override.



Whats dis-advantages of inheritance?

super class and child class are strongly connected.



Whats dis-advantages of class?

Same Obejct/memory location is shared among two or more obejcts if they point to same obejct.

If one changes onother will have that new changes even if you don't want.

Memory and threading issuses



With value type we don't need to worry about memory leak/reference cycle and Multi-threading issues.

Value types are free from all these defects.



Use  value type  and Protocols as much as you can. Unless you don't have a option.

 

Strongly connected/ Decoupling  is consider as bad in Software development.



## More isolation more easy to test

Protocol and value type allows isolation.



Think protocol like `Sword Logo ADT`. You attach and de-attach it to any other pieces and then that piece have Sword.

Easy to attach, deattach ie re-usability and easy to test and easy to modify, easy to extend  capability/functionality.

(These all consider as best practices in Software developemt)



Example:- Equatable , Hashable



```swift

struct Person {
    
}



```



 Lets assume above strcut does not have logic to compare two object 
and you ship this to app store or you are not allowed to modify it or you doesn't have source code for Eg String, Int

Then how you extend its Equality capacity?
If its class then inherit from it and Just for one extra capability we need to inherit and if required then override hundered lines of code.

and then find where we are using Person and changed it to new type.



Such Practices are consider as bad Practices.



With Protocol you can extend functionality of a type without touching or modifiying any line of code using Protocol.

You can add much as you need functonality to a existing type using protocol(s).





## Consider as Bad so Always try to avoid

Coupled -> Bad for testing

Reference type, memory shared, multiple owners, multi-threading issues, memory. 

Modification to existing type.

Modification in code base like changing existing object with other obejct.

Specific type is bad. Generic is much better.

No flexibility -> less re-usability

Duplicated

## Consider as Good So Always Aim for these

Value type 

No modification

isolation  ->Easy to test

easy to modifiy  and easy to extend functionality without modifying existing codes or subclasing.  -> `Use Protocol, extenson , generic and Struct`



Protoocl with associated type is much better thang fixed type.

First Design Protocol Adt

then provide and default implementation using extension

When ever you need Magic power of That protocol Just Inject it like Logo 





**Benefits of Protocol-Oriented Programming:**

- All classes are decoupled from each other
- Separating the concerns of declaration from implementation
- Reusability
- Testability



Protocol-oriented programming enables writing code that is more modular, decoupled, and flexible, compared to traditional object-oriented programming.