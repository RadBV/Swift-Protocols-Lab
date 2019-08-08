
## Protocols Lab

## Instructions for lab submission

1. Fork the assignment repo
1. Clone your Fork to your machine
1. Complete the lab
1. Push your changes to your Fork
1. Submit a Pull Request back to the assignment repo
1. Paste a link of the pull request on Canvas and submit


<br>

> Questions adapted from [Swift student lessons: 4 - Tables and Persistence -> 1 - Protocols](https://developer.apple.com/go/?id=app-dev-swift-student)

## Question 1

a. Create a `Human` class with two properties:
- `name` of type String
- `age` of type Int.

Then create an initializer for the class and create two `Human` instances.

```swift
class Human {
    var name: String
    var age: Int

    init(name: String, age: Int) {
        self.name = name
        self.age = age
    }
}

var david = Human(name: "David Rifkin", age: 300)
var olimpia = Human(name: "Olimpia Compean", age: 30)
```

b. Make the `Human` class adopt the CustomStringConvertible protocol. Then print both of your previously initialized
`Human` objects.

```swift
class Human: CustomStringConvertible {
    var description: String
    var name: String
    var age: Int

    init(name: String, age: Int, description: String) {
        self.name = name
        self.age = age
        self.description = description
    }
}

var david = Human(name: "David Rifkin", age: 300, description: "a cool guy")
var olimpia = Human(name: "Olimpia Compean", age: 30, description: "the best")

print(david)
print(olimpia)
```

c. Make the `Human` class adopt the Equatable protocol. Two instances of `Human` should be considered equal
if their names and ages are identical to one another. Print the result of a boolean expression
evaluating whether or not your two previously initialized `Human` objects are equal to eachother
(using ==). Then print the result of a boolean expression evaluating whether or not your two
previously initialized `Human` objects are not equal to eachother (using !=).

```swift
class Human: CustomStringConvertible, Equatable {
    static func == (lhs: Human, rhs: Human) -> Bool {
        return lhs.age == rhs.age && lhs.name == rhs.name
    }

    var description: String
    var name: String
    var age: Int

    init(name: String, age: Int, description: String) {
        self.name = name
        self.age = age
        self.description = description
    }
}

var david = Human(name: "David Rifkin", age: 300, description: "a cool guy")
var olimpia = Human(name: "Olimpia Compean", age: 30, description: "the best")

print(david == olimpia)
print(david != olimpia)
```

d. Make the `Human` class adopt the `Comparable` protocol. One `Human` is greater than another `Human` if its age is bigger. Create another
three instances of a `Human`, then create an array called people of type [`Human`] with all of the
`Human` objects that you have initialized.

Create a new array called sortedPeople of type [`Human`] that is the people array sorted by age.

```swift
class Human: CustomStringConvertible, Equatable, Comparable {
    static func < (lhs: Human, rhs: Human) -> Bool {
        return lhs.age > rhs.age
    }

    static func == (lhs: Human, rhs: Human) -> Bool {
        return lhs.age == rhs.age && lhs.name == rhs.name
    }

    var description: String
    var name: String
    var age: Int

    init(name: String, age: Int, description: String) {
        self.name = name
        self.age = age
        self.description = description
    }
}

var me = Human(name: "Rad", age: 21, description: "a clown")
var tut = Human(name: "TutanKhamun", age: 3360, description: "young pharoah of egypt (ruled c. 1332 – 1323 BC)")
var god = Human(name: "God", age: 8999999999999989999, description: "God")

var people: [Human] = [tut,god,me]
var sortedPeople = people.sorted()
print(sortedPeople)
```

</br> </br>


## Question 2

a. Create a protocol called `Vehicle` with two requirements:
- a nonsettable `numberOfWheels` property of type Int,
- a function called drive().

```swift
protocol Vehicle {
    var numberOfWheels: Int {get}
    func drive()
}
```

b. Define a `Car` struct that implements the `Vehicle` protocol. `numberOfWheels` should return a value of 4,
and drive() should print "Vroom, vroom!" Create an instance of `Car`, print its number of wheels,
then call drive().

```swift
struct Car: Vehicle {
    var numberOfWheels: Int

    func drive() {
        print("Vroom, vroom!")
    }
}

var clownMobile = Car(numberOfWheels: 4)

print(clownMobile.numberOfWheels)
clownMobile.drive()
```

c. Define a Bike struct that implements the `Vehicle` protocol. `numberOfWheels` should return a value of 2,
and drive() should print "Begin pedaling!". Create an instance of Bike, print its number of wheels,
then call drive().

```swift
struct Bike: Vehicle {
    var numberOfWheels: Int

    func drive() {
        print("Behin pedaling!")
    }
}

var tricycleButOneWheelIsMissing = Bike(numberOfWheels: 2)

print(tricycleButOneWheelIsMissing.numberOfWheels)
tricycleButOneWheelIsMissing.drive()
```

</br> </br>


## Question 3
// Given the below two protocols, create a struct for penguin(a flightless bird) and an eagle.

Give your structs some properties and have them conform to the appropriate protocols.

```swift
protocol Bird {
 var name: String { get }
 var canFly: Bool { get }
}

protocol Flyable {
 var airspeedVelocity: Double { get }
}
```

```swift
struct Penguin: Bird {
    var name: String
    var canFly: Bool
    var waddleSpeed: Double
}

struct eagle: Bird, Flyable {
    var name: String
    var canFly: Bool
    var airspeedVelocity: Double
    var hasIntenseStare: Bool
}
```

</br> </br>

## Question 4

a. Create a protocol called `Transformation`.  The protocol should specify a mutating method called transform

```swift
protocol Transformation {
    mutating func transform()
}
```

b. Make an enum called `SuperHero` that conforms to `Transformation` with cases `notHulk` and `hulk`

```swift
enum SuperHero: Transformation {
    func transform() {
         <#code#>
    }
    case hulk
    case notHulk

}
```
c. Create an instance of it named `bruceBanner`. Make it so that when the transform function is called that bruceBanner turns from
`.notHulk` to `.hulk.``

```swift
enum SuperHero: Transformation {
    mutating func transform() {
        self = .hulk
    }
    case hulk
    case notHulk
}

// Example Output:
var bruceBanner = SuperHero.notHulk

bruceBanner.transform() . // hulk

bruceBanner.transform()  // notHulk
```

</br> </br>


## Question 5

a. Create a protocol called `Communication`

```swift
protocol Communication {
    
}
```

b. Give it a property called `message`, of type String, and assign it an explicit getter.

```swift
protocol Communication {
    var message: String { get }
    
    func talk()
}
```
c. Create three Classes. `Cow`, `Dog`, `Cat`.

```swift
class Cow {

}

class Dog {

}

class Cat {

}
```

d. Have your three classes conform to `Communication`

```swift
class Cow: Communication {
    var message: String 

    func talk() {
        
    }
}

class Dog: Communication {
    var message: String 

    func talk() {
        print(message)
    }
}

class Cat: Communication {
    var message: String

    func talk() {
        print(message)
    }
}
```

e. `message` should return a unique message for each animal when talk is called.

```swift
class Cow: Communication {
    var message: String = "Moo"

    func talk() {
        print(message)
    }
}

class Dog: Communication {
    var message: String = "Woof"

    func talk() {
        print(message)
    }
}

class Cat: Communication {
    var message: String = "Meow"

    func talk() {
        print(message)
    }
}
```

f. Put an instance of each of your classes in an array.

g. Iterate over the array and have them print their `message` property


## Question 6

The HeartRateReceiver class below represents a very simplified example of a class dedicated to receiving information from fitness tracking hardware with monitoring heart rate. The function startHeartRateMonitoringExample will generate random heart rates and assign them to currentHR, simulating how an instance of HeartRateReceiver may pick up on new heart rate readings at specific intervals.

HeartRateViewController below is a view controller that will present the heart rate information to the user. Throughout the exercises below you'll use the delegate pattern to pass information from an instance of HeartRateReceiver to the view controller so that anytime new information is obtained it is presented to the user.

```swift
class HeartRateReceiver {
    var currentHR: Int? {
        didSet {
            if let currentHR = currentHR {
                print("The most recent heart rate reading is \(currentHR).")
            } else {
                print("Looks like we can't pick up a heart rate.")
            }
        }
    }

    func startHeartRateMonitoringExample() {
        for _ in 1...10 {
            let randomHR = 60 + Int.random(in: 0...15)
            currentHR = randomHR
            Thread.sleep(forTimeInterval: 2)
        }
    }
}

class HeartRateViewController: UIViewController {
    var heartRateLabel: UILabel = UILabel()
}
```

First, create an instance of HeartRateReceiver and call startHeartRateMonitoringExample. Notice that every two seconds currentHR get set and prints the new heart rate reading to the console.

In a real app, printing to the console does not show information to the user. You need a way of passing information from the HeartRateReceiver to the HeartRateViewController. To do this, create a protocol called HeartRateReceiverDelegate that requires a method heartRateUpdated(to bpm:) where bpm is of type Int and represents the new rate as beats per minute. Since playgrounds read from top to bottom and the two previously declared classes will need to use this protocol, you'll need to declare this protocol above the declaration of HeartRateReceiver.

Now make HeartRateViewController adopt the protocol you've just created. Inside the body of the required method you should set the text of heartRateLabel and print "The user has been shown a heart rate of <INSERT HEART RATE HERE>."

Now add a property called delegate to HeartRateReceiver that is of type HeartRateReceiverDelegate?. In the didSet of currentHR where currentHR is successfully unwrapped, call heartRateUpdated(to bpm:) on the delegate property.

Finally, return to the line of code just after you initialized an instance of HeartRateReceiver. Initialize an instance of HeartRateViewController. Then, set the delegate property of your instance of HeartRateReceiver to be the instance of HeartRateViewController that you just created. Wait for your code to compile and observe what is printed to the console. Every time that currentHR gets set, you should see both a printout of the most recent heart rate, and the print statement stating that the heart rate was shown to the user.
