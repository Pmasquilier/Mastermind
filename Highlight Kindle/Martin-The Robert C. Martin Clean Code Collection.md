---
kindle-sync:
  bookId: '13350'
  title: The Robert C. Martin Clean Code Collection (Collection)
  author: 'Martin, Robert C.'
  highlightsCount: 46
---
# The Robert C. Martin Clean Code Collection
## Metadata
* Author: [[Martin, Robert C.]]

## Highlights
Avoid Disinformation — location: [1215]() ^ref-34337

---
Beware of using names which vary in small ways. — location: [1224]() ^ref-26701

---
Make Meaningful Distinctions — location: [1239]() ^ref-35626

---
getActiveAccount();    getActiveAccounts();    getActiveAccountInfo(); — location: [1265]() ^ref-51562

---
So make your names pronounceable. — location: [1274]() ^ref-40330

---
This matters because programming is a social activity. — location: [1275]() ^ref-8826

---
Use Searchable Names — location: [1287]() ^ref-54194

---
Calling it ShapeFactoryImp, or even the hideous CShapeFactory, is preferable to encoding the interface. — location: [1338]() ^ref-27535

---
Classes and objects should have noun or noun phrase — location: [1353]() ^ref-47413

---
A class name should not be a verb. — location: [1356]() ^ref-3816

---
Methods should have verb or verb phrase names — location: [1357]() ^ref-56301

---
When constructors are overloaded, use static factory methods with names that describe the arguments. For example,    Complex fulcrumPoint = Complex.FromRealNumber(23.0); is generally better than    Complex fulcrumPoint = new Complex(23.0); — location: [1363]() ^ref-15926

---
Pick one word for one abstract concept and stick with it. For instance, it’s confusing to have fetch, retrieve, and get as equivalent methods of different classes. — location: [1375]() ^ref-23890

---
one word per concept” rule, — location: [1390]() ^ref-8607

---
You can add context by using prefixes: addrFirstName, addrLastName, addrState, and so on. — location: [1419]() ^ref-57778

---
Of course, a better solution is to create a class named Address. — location: [1421]() ^ref-28976

---
Functions should hardly ever be 20 lines long. — location: [1553]() ^ref-45488

---
the indent level of a function should not be greater than one or two. — location: [1574]() ^ref-3351

---
FUNCTIONS SHOULD DO ONE THING. THEY SHOULD DO IT WELL. THEY SHOULD DO IT ONLY. — location: [1583]() ^ref-33893

---
So, another way to know that a function is doing more than “one thing” is if you can extract another function from it with a name that is not merely a restatement of — location: [1607]() ^ref-43894

---
My general rule for switch statements is that they can be tolerated if they appear only once, are used to create polymorphic objects, and are hidden behind an inheritance relationship so that the rest of the system can’t see them — location: [1679]() ^ref-33276

---
There may be no more than one switch statement for a given type of selection. The cases in that switch statement must create polymorphic objects that take the place of other such switch statements in the rest of the system. — location: [7451]() ^ref-51587

---
the Law of Demeter says that a method f of a class C should only call the methods of these: • C • An object created by f • An object passed as an argument to f • An object held in an instance variable of C — location: [2921]() ^ref-35395

---
make up for the liberal use of Maps. A — location: [3268]() ^ref-49493

---
cleaner way to use Map might look like the following. No user of Sensors would care one bit if generics were used or not. That choice has become (and always should — location: [3269]() ^ref-22573

---
be) an implementation detail.    public class Sensors {      private Map sensors = new HashMap();      public Sensor getById(String id) {        return (Sensor) sensors.get(id);      }      // — location: [3270]() ^ref-2248

---
First Law You may not write production code until you have written a failing unit test. Second Law You may not write more of a unit test than is sufficient to fail, and not compiling is failing. Third Law You may not write more production code than is sufficient to pass the currently failing test. — location: [3423]() ^ref-42985

---
I think the best thing we can say is that the number of asserts in a test ought to be minimized. — location: [3629]() ^ref-54651

---
Perhaps a better rule is that we want to test a single concept in each test function. — location: [3631]() ^ref-50178

---
So probably the best rule is that you should minimize the number of asserts per concept and test just one concept per test function. — location: [3659]() ^ref-60457

---
F.I.R.S.T.8 Clean tests follow five other rules that form the above acronym: Fast Tests should be fast. They should run quickly. — location: [3661]() ^ref-1147

---
If a test in the same package needs to call a function or access a variable, we’ll make it protected or package scope. However, we’ll first look for a way to maintain privacy. Loosening encapsulation is always a last resort. — location: [3707]() ^ref-12982

---
The name of a class should describe what responsibilities it fulfills. In fact, naming is probably the first way of helping determine class size. If we cannot derive a concise name for a class, then it’s likely too large. The more ambiguous the class name, the more likely it has too many responsibilities. For example, class names including weasel words like Processor or Manager or Super often hint at unfortunate aggregation of responsibilities. We should also be able to write a brief description of the class in about 25 words, without using the words “if,” “and,” “or,” or “but.” — location: [3766]() ^ref-6234

---
systems to be composed of many small classes, not a few large ones. Each small class encapsulates a single responsibility, has a single reason to change, and collaborates with a few others to achieve the desired system behaviors. — location: [3806]() ^ref-39987

---
According to Kent, a design is “simple” if it follows these rules: • Runs all the tests • Contains no duplication • Expresses the intent of the programmer • Minimizes the number of classes and methods — location: [4505]() ^ref-29049

---
“the Boy Scout rule”: Always check in a module cleaner than when you checked it out. Always make some random act of kindness to the code whenever you see it. — location: [10824]() ^ref-37671

---
Design patterns. You ought to be able to describe all 24 patterns in the GOF book and have a working knowledge of many of the patterns in the POSA books. — location: [10881]() ^ref-14342

---
• Design principles. You should know the SOLID principles and have a good understanding of the component principles. — location: [10882]() ^ref-17177

---
Methods. You should understand XP, Scrum, Lean, Kanban, Waterfall, Structured Analysis, and Structured Design. — location: [10884]() ^ref-20190

---
Disciplines. You should practice TDD, Object-Oriented design, Structured Programming, Continuous Integration, and Pair Programming. — location: [10886]() ^ref-17364

---
Artifacts: You should know how to use: UML, DFDs, Structure Charts, Petri Nets, State Transition Diagrams and Tables, flow charts, and decision tables. — location: [10887]() ^ref-12393

---
Think of the kata as a 10-minute warm-up exercise in the morning and a 10-minute cool-down in the evening. — location: [10912]() ^ref-47930

---
Professionals are not required to say yes to everything that is asked of them. However, they should work hard to find creative ways to make “yes” possible. When professionals say yes, they use the language of commitment so that there is no — location: [11593]() ^ref-2226

---
You are not allowed to write any production code until you have first written a failing unit test. You are not allowed to write more of a unit test than is sufficient to fail—and not — location: [11961]() ^ref-5066

---
compiling is failing. You are not allowed to write more production code that is sufficient to pass the currently failing unit test. — location: [11963]() ^ref-11759

---
This is called trivariate analysis: — location: [12939]() ^ref-13407

---
