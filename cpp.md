# Craftsmanship - C++

> Credit: Szabo Bence, my dearest colleague)

## Books

- [Effective Modern C++](https://www.google.com/books/edition/Effective_Modern_C++/I5_joAEACAAJ?hl=en)
- [A Tour of C++](https://books.google.com/books?id=-VNsAQAAQBAJ&printsec=frontcover&dq=c%2B%2B&hl=en&newbks=1&newbks_redir=1&sa=X&ved=2ahUKEwiYroiS0q3wAhVTPn0KHYbsDaQQ6AEwAHoECAEQAg)

## CppCon

- [Slides](https://github.com/CppCon/CppCon2020)
- [Videos](https://www.youtube.com/user/CppCon/videos)

### Back to basics

"Zero to hero" videos that cover a specific topic in an
easy-to-understand way. [CppCon Back to Basics -
playlist](https://www.youtube.com/playlist?list=PL5qoVlA-tv09ykIIPHP9N6vgJaFPnYWCa)

- [CppCon 2019: Dan Saks “Back to Basics: Function and Class Templates”](https://www.youtube.com/watch?v=LMP_sxOaz6g&list=PL5qoVlA-tv09ykIIPHP9N6vgJaFPnYWCa&index=4)
- [CppCon 2019: Dan Saks “Back to Basics: Const as a Promise”](https://www.youtube.com/watch?v=NZtr93iL3R0&list=PL5qoVlA-tv09ykIIPHP9N6vgJaFPnYWCa&index=5)
- [CppCon 2019: Ben Saks “Back to Basics: Understanding Value Categories”](https://www.youtube.com/watch?v=XS2JddPq7GQ&list=PL5qoVlA-tv09ykIIPHP9N6vgJaFPnYWCa&index=6)
- [CppCon 2019: Arthur O'Dwyer “Back to Basics: Lambdas from Scratch”](https://www.youtube.com/watch?v=3jCOwajNch0&list=PL5qoVlA-tv09ykIIPHP9N6vgJaFPnYWCa&index=10)
- [CppCon 2019: Jason Turner “C++ Code Smells”](https://www.youtube.com/watch?v=f_tLQl0wLUM&list=PL5qoVlA-tv09ykIIPHP9N6vgJaFPnYWCa&index=15)

### Testing

- [CppCon 2019: Fedor Pikus “Back to Basics: Test-driven
 Development”](https://www.youtube.com/watch?v=RoYljVOj2H8)
  - what's a unit test
  - how to unit test
  - what to test
  - how to write testable code (from 29min)

- [The Science of Unit Tests - Dave Steffen - CppCon 2020](https://www.youtube.com/watch?v=FjwayiHNI1w&t=0s)
  - builds on the previous talk
  - testing private stuff
  - testing interfaces
  - paradoxes of testing units thru interfaces
  - BDD
  - how to interpret correctness of a unit test

- [CppCon 2015: T. Winters & H. Wright “All Your Tests are Terrible..."](https://www.youtube.com/watch?v=u5senBJUkPc)
  - a funny take on 'how to test'
  - a case study of bad tests at google

### Lifetime safety

- [CppCon 2018: Jason Turner “Surprises in Object Lifetime”](https://www.youtube.com/watch?v=uQyT-5iWUow)

### Performance

- [CppCon 2014: Mike Acton "Data-Oriented Design and C++"](https://www.youtube.com/watch?v=rX0ItVEVjHc)
  - Data is king, everything else is secondary
- [CppCon 2018: Stoyan Nikolov “OOP Is Dead, Long Live Data-oriented Design”](https://www.youtube.com/watch?v=yy8jQgmhbAU)
  - example for OOP vs data oriented design
- [CppCon 2014: Andrei Alexandrescu "Optimization Tips - Mo' Hustle Mo'Problems"](https://www.youtube.com/watch?v=Qq_WaiwzOtI)
  - micro optimizations in large scale code at facebook
- [Fastware - Andrei Alexandrescu](https://www.youtube.com/watch?v=o4-CwDo2zpg)
  - micro optimization techniques
  - effect of cache and modern pipelined CPUs
- [CppCon 2019: Andrei Alexandrescu “Speed Is Found In The Minds of People"](https://www.youtube.com/watch?v=FJJTYQYB1JQ)
  - ultra-optimized sorting algorithm
  - effects of cache
  - how to measure performance theoretically vs in reality
- [CppCon 2016: Jason Turner “Practical Performance Practices"](https://www.youtube.com/watch?v=uzF4u9KgUWI)

### Bugs

- [CppCon 2017: Louis Brandy “Curiously Recurring C++ Bugs at Facebook”](https://www.youtube.com/watch?v=lkgszkPnV8g)
  - a case study of common bugs at facebook
  - how to mitigate bugs that happen every 2 days

### Architecture

- [CppCon 2018: Titus Winters “Modern C++ Design (part 1 of 2)”](https://www.youtube.com/watch?v=xTdeZ4MxbKo)

- [CppCon 2018: Titus Winters “Modern C++ Design (part 2 of 2)”](https://www.youtube.com/watch?v=tn7oVNrPM8I)
  - designing APIs, types
  - how to communicate with the user thru design

- [CppCon 2016: John Lakos “Advanced Levelization Techniques (part 1 of 3)"](https://www.youtube.com/watch?v=QjFpKJ8Xx78)
- [CppCon 2016: John Lakos “Advanced Levelization Techniques (part 2 of 3)"](https://www.youtube.com/watch?v=fzFOLsFASjU)
- [CppCon 2016: John Lakos “Advanced Levelization Techniques (part 3 of 3)"](https://www.youtube.com/watch?v=NrARQ7rHV-c)
- tldr version: [Lakos’20: The “Dam” Book is Done! - John Lakos - CppCon 2020](https://www.youtube.com/watch?v=d3zMfMC8l5U)
  - How to handle large systems
  - How to do packaging

### Templates

- [C++Now 2018: Odin Holmes “C++ Mixins: Customization Through Compile
 Time
 Composition”](https://www.youtube.com/watch?v=wWZi_wPyVvs)

### std::algorithms

- [CppCon 2018: Jonathan Boccara “105 STL Algorithms in Less Than an Hour”](https://www.youtube.com/watch?v=2olsGf6JIkU)
  - an overview of all the stl algorithms

### Custom memory allocators

- [CppCon 2015: Andrei Alexandrescu “std::allocator...”](https://www.youtube.com/watch?v=LIb3L4vKZ7U)
  - what's an allocator?
  - custom allocators
  - jokes

- [C++ Weekly - Ep 222 - 3.5x Faster Standard Containers With PMR!](https://www.youtube.com/watch?v=q6A7cKFXjY0)
- [C++ Weekly - Ep 250 - Custom Allocation - How, Why, Where (Huge multi threaded gains and more!)](https://www.youtube.com/watch?v=5VrX_EXYIaM)
- [C++ Weekly - Ep 248 - Understand the C++17 PMR Standard Allocators and Track All the Things](https://www.youtube.com/watch?v=Zt0q3OEeuB0)
- [C++ Weekly - Ep 236 - Creating Allocator-Aware Types](https://www.youtube.com/watch?v=2LAsqp7UrNs)
- [CppCon 2019: John Lakos “Value Proposition: Allocator-Aware (AA) Software”](https://www.youtube.com/watch?v=ebn1C-mTFVk)

### How features are born

- [CppCon 2015: Andrei Alexandrescu “Declarative Control Flow"](https://www.youtube.com/watch?v=WjTrfoiB0MQ)
  - intro to the upcoming std::scope\_exit feature

- [CppCon 2018: Andrei Alexandrescu “Expect the expected”](https://www.youtube.com/watch?v=PH4WBuE1BHI)
  - upcoming std::expected
  - exceptions vs error codes
  - how to get the best of exceptions and error codes

### Introspection - this feature is not part of c++ yet

- [The next big Thing - Andrei Alexandrescu - Meeting C++ 2018 Opening Keynote](https://www.youtube.com/watch?v=tcyb1lpEHm0)
  - retrospective of "big things" in c++
  - idea on what the future should hold for us

### Concurency

- [CppCon 2017: Fedor Pikus “C++ atomics, from basic to advanced. What do they really do?”](https://www.youtube.com/watch?v=ZQFzMfHIxng)
- [CppCon 2016: Fedor Pikus “The speed of concurrency (is lock-free faster?)"](https://www.youtube.com/watch?v=9hJkWwHDDxs)

### Value categories

- [CppCon 2019:Ben Saks “Back to Basics: Understanding Value Categories”](https://www.youtube.com/watch?v=XS2JddPq7GQ&list=PL5qoVlA-tv09ykIIPHP9N6vgJaFPnYWCa&index=6)
- [CppCon 2015: John Lakos “Value Semantics: It ain't about the syntax!, Part I"](https://www.youtube.com/watch?v=W3xI1HJUy7Q)
- [CppCon 2015: John Lakos “Value Semantics: It ain't about the syntax!, Part II"](https://www.youtube.com/watch?v=0EvSxHxFknM)
  - What's a 'value' ?
  - How to implement a value type
  - What other categories are there?
