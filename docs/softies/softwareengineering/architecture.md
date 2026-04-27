- Software is made of software.

- Architecture represents the significant design decisions that shape a system, where significant is measured by cost of change. (—Grady Booch)

- The only way to go fast, is to go well. (—Robert C. Martin)

- Alan Turing wrote the first machine code in 1946

It doesn’t take a huge amount of knowledge and skill to get a program
working. Kids in high school do it all the time. Young men and women in
college start billion-dollar businesses based on scrabbling together a few lines
of PHP or Ruby. It works because getting something to work—once—just isn’t that hard.
Getting it right is another matter entirely. Getting software right is hard. It
takes knowledge and skills that most young programmers haven’t yet
acquired. It requires thought and insight that most programmers don’t take
the time to develop. It requires a level of discipline and dedication that most
programmers never dreamed they’d need. Mostly, it takes a passion for the
craft and the desire to be a professional.
When software is done right, it requires a fraction of the human resources to
create and maintain. Changes are simple and rapid. Defects are few and far
between. Effort is minimized, and functionality and flexibility are maximized.

- Architecture (used in the high-level context) = Design (low-level context)
- all the little details that support all the high-level decisions

- The goal of software architecture is to minimize the human resources required to build and maintain the required system.

- The bigger lie that developers buy into is the notion that writing messy code makes them go fast in the short term, and just slows them down in the long term. The fact is that making messes is always slower than staying clean, no matter which time scale you are using.

- To take software architecture seriously, you need to know what good software architecture is. To build a system with a design and an architecture that minimize effort and maximize productivity, you need to know which attributes of system architecture lead to that end.

- Every software system provides two different values to the stakeholders: behavior and structure. Software developers are responsible for ensuring that both those values remain high. Unfortunately, they often focus on one to the exclusion of the other. Even more unfortunately, they often focus on the lesser of the two values, leaving the software system eventually valueless.

### Behavior

The first value of software is its behavior. Programmers are hired to make
machines behave in a way that makes or saves money for the stakeholders. We
do this by helping the stakeholders develop a functional specification, or
requirements document. Then we write the code that causes the stakeholder’s
machines to satisfy those requirements.
When the machine violates those requirements, programmers get their
debuggers out and fix the problem.
Many programmers believe that is the entirety of their job. They believe their
job is to make the machine implement the requirements and to fix any bugs.
They are sadly mistaken.

- 'ware' means product
  Software was invented to be “soft.” It was intended to be a way to easily
  change the behavior of machines. If we’d wanted the behavior of machines to
  be hard to change, we would have called it hardware.
  The difficulty in making such a change should be proportional only to the scope of the change, and not to the shape of the change.

It is this difference between scope and shape that often drives the growth in
software development costs. It is the reason that costs grow out of proportion
to the size of the requested changes. It is the reason that the first year of
development is much cheaper than the second, and the second year is much
cheaper than the third.

From the stakeholders’ point of view, they are simply providing a stream of
changes of roughly similar scope. From the developers’ point of view, the
stakeholders are giving them a stream of jigsaw puzzle pieces that they must
fit into a puzzle of ever-increasing complexity. Each new request is harder
to fit than the last, because the shape of the system does not match the shape
of the request.

### The Greater Value

- Is it more important for the software system to work, or is it more important for the software system to be easy to change?

- I have two kinds of problems, the urgent and the important. The urgent are not important, and the important are never urgent. (-Dwight D. Eisenhower)

- The first value of software—behavior—is urgent but not always particularly important.
- The second value of software—architecture—is important but never particularly urgent.

The business managers and developers often fail to separate those
features that are urgent but not important from those features that truly are
urgent and important. This failure then leads to ignoring the important
architecture of the system in favor of the unimportant features of the system.

Software architects are, by virtue of their job description, more focused on the
structure of the system than on its features and functions. Architects create an
architecture that allows those features and functions to be easily developed,
easily modified, and easily extended.

### little bit og history

In 1938, Alan Turing laid the foundations of what was to become computer
programming. He was not the first to conceive of a programmable machine,
but he was the first to understand that programs were simply data. By 1945,
Turing was writing real programs on real computers in code that we would
recognize (if we squinted enough). Those programs used loops, branches,
assignment, subroutines, stacks, and other familiar structures. Turing’s
language was binary.

Since those days, a number of revolutions in programming have occurred.
One revolution with which we are all very familiar is the revolution of
languages. First, in the late 1940s, came assemblers. These “languages”
relieved the programmers of the drudgery of translating their programs into
binary. In 1951, Grace Hopper invented A0, the first compiler. In fact, she
coined the term compiler. Fortran was invented in 1953. What followed was an unceasing flood of new programming languages—COBOL, PL/1, SNOBOL, C, Pascal, C++, Java, ad infinitum.

Another, probably more significant, revolution was in programming
paradigms. Paradigms are ways of programming, relatively unrelated to
languages. A paradigm tells you which programming structures to use, and
when to use them.

### Paradigm Overview

- The paradigms tell us what not to do, more than they tell us what to do.

#### Structured

- Structured Programming: discovered by Edsger Wybe Dijkstra in 1968, replacing replaced goto jumps with if/then/else and do/while/until constructs

**Structured programming imposes discipline on direct transfer of control.**

Structured programming forces us to recursively decompose a program into a
set of small provable functions. We can then use tests to try to prove those
small provable functions incorrect. If such tests fail to prove incorrectness,
then we deem the functions to be correct enough for our purposes.

- instead of using **goto** statement, use:
  - Sequence → steps executed in order
  - Selection → decisions (if statements)
  - Iteration → loops (for/while)

- The main idea: programs should flow logically, like a well-written story.

#### Object-oriented

- Object-oriented Programming: discovered by Ole Johan Dahl and Kristen Nygaard in 1966

**Object-oriented programming imposes discipline on indirect transfer of control.**

- proper mixture of Encapsulation, Inheritance, Polymorphism

#### Functional

- Functional Programming: the direct result of the work of Alonzo Church, who in 1936 invented l-calculus while pursuing the same mathematical problem that was motivating Alan Turing at the same time

**Functional programming imposes discipline upon assignment.**

- We use polymorphism as the mechanism to cross architectural boundaries; we use functional programming to impose discipline on the location of and access to data; and we use structured programming as the algorithmic foundation of our modules.

**Notice how well those three align with the three big concerns of architecture: function, separation of components, and data management.**
