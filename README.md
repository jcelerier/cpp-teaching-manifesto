# The C++ Teaching Manifesto

Teaching C++ is a hard task, for students as well as for teachers.
This manifesto intends to ensure that this task is not made unintentionally harder for both parties, 
by providing up-to-date best practices for teaching.


#### 1. I will teach C++ as a high-level language.
* Too many courses take the approach of presenting C++ on the same level of abstraction than C. This is severely misguided.
  * C++ programs are written against the C++ abstract machine, not your classroom's CPUs, and compilers *will* optimize code with the assumptions of the abstract machine in mind.
  * C++ allows for arbitrarily high levels of abstractions, with generally no runtime penalty for optimized code, if either inlining or LTO are leveraged.
  * https://www.bfilipek.com/2017/10/expressive-cpp17-results.html

#### 2. I will teach the core concepts and values of C++
* Value semantics.
* Const-correctness.
* Ownership and RAII, resource management.
* Zero-cost abstractions.
* Generic programming and how to leverage the type system to provide maximal compile-time guarantees on your program.
  * In particular, not doing at run-time what can be done at compile time.

#### 3. I will refer to and keep up-to-date with current best practices
* C++ authors and designers have created the C++ Core Guidelines, in order to show what is the best practice, in a language with 40 years of legacy baggage https://github.com/isocpp/CppCoreGuidelines
* https://github.com/lefticus/cppbestpractices

#### 4. I will not teach using outdated revisions of the C++ standard.
* ISO rules mandata that the *only* valid standard at a given point in time is the last one. We don't build new houses with electric plugs from 50 years ago.
* C++ has a three years release cadence : by the time the students are on the job market, what was considered avant-garde during their classes will be mainstream.
* It is not necessary to use non-released standards, but it can be interesting to at least look at them - that's the standards which will be in effect when the students are out of school ! 

#### 5. I will not use outdated tooling to teach my students
* Windows : use msys2 with the latest clang, gcc, or an MSVC recent enough to support motion 4. 
* Ubuntu or Debian : if a recent distribution is not available, use the packages from https://apt.llvm.org/
* Mac : use a recent macOS with the latest Xcode, or install the latest gcc or llvm from Homebrew if macOS cannot be upgraded.

#### 6. I will not teach C++ as an object-oriented language
* Because it is not. By the own word of its creator, it is a multi-paradigm language. 
* Fun fact : C++ is a fairly advanced functional language, thanks to type-level computations and some level of dependent typing (non-type template parameters).
* C++ can be leveraged to study almost the whole history of programming, so let's leverage that and provide nice examples to our students.

#### 7. I will not teach dialectal or platform-specific C++
* No "C/C++" : https://www.youtube.com/watch?v=YnWhqhNdYyk
* No C-with-classes : just teach C or Java if you really want to do that.
* No "Java/C++". Hint : if you are writing `new std::string`, there is something wrong.
* No -fno-exceptions : exceptions are a core part of C++. They give all their meaning to RAII, and except on 32-bit Windows are faster on the happy path than error codes. 
  * It's easier to learn to not use exceptions if you already know them, than to learn to use exceptions if you don't.
* No conio.h / iostream.h / graphics.h / whatever DOS-era API you can find.

#### 8. I will not teach outdated software development patterns
* Multiple classical development patterns were over the years integrated in various programming language, either as language or library features.
* Closed polymorphism : visitor pattern -> now can be done with std::variant
* Strategy pattern : std::function 

#### 9. I will not teach volatile as a multithread synchronization mechanism
* Long story short : it does not work in the general case.
* http://cxx.isvolatileusefulwiththreads.com/	
* Use atomics.

