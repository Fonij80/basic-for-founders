# Understanding Artificial Intelligence

- Artificial intelligence is sometimes presented as a new revolution. It seems possible to provide machines with self-awareness, to make them capable of thinking for themselves, even to surpass us.

- Computer science is the science of processing information. It’s about building, creating, and inventing machines that automatically process all kinds of information, from numbers to text, images, or video.

- To process the information, the computer applies a method called an algorithm.

- A computer is a machine that processes data provided on a physical medium (for example a perforated card, a magnetic tape, a compact disc) by following a set of instructions written on a physical medium (the same medium as the data, usually): it’s a machine that carries out algorithms.

- Charles Babbage Idea (1791–1871): creating a machine that can carry out different algorithms

## The All-purpose Machine

- Turing machine: mathematical model of computation in 1936 ny Alan Turing, he showed that his machine could reproduce any algorithm

- A Turing machine consists of a strip of tape on which symbols can be written. To give you a better idea, imagine a 35 mm reel of film with small cells into which you can put a photo. With a Turing machine, however, we don’t use photos. Instead, we use an alphabet – in other words, a list of symbols (for example 0 and 1, which are computer engineers’ favorite symbols). In each cell, we can write only one symbol. For the Turing machine to work, you need to give it a set of numbered instructions, as shown below:

- Instruction 1267:
  - Symbol 0 → Move tape one cell to the right, Go to instruction 3146

  - Symbol 1 → Write 0, Move tape one cell to the left, Resume instruction 1267.

- computer works exactly like a Turing machine: has a memory (equivalent to the Turing machine’s “tape”), it reads symbols contained in memory cells, and it carries out specific instructions with the help of electronic wires.

### Recap

- A computer is a machine equipped with a memory on which two things are recorded: data and an algorithm, coded in a particular language, which specifies how the data is to be processed. An algorithm written in a language that can be interpreted by a machine is called a computer program, and when the machine carries out what is described in the algorithm, we say that the computer is running the program.

### Where does AI fit in all this?

- According to Minsky (1968), who helped found the discipline in the 1950s, AI is “the building of computer programs which perform tasks which are, for the moment, performed in a more satisfactory way by humans because they require high level mental processes such as: perception learning, memory organization and critical reasoning.”

- machine learning: an AI technique

- For this reason, an AI program using machine learning can only produce a “good” program if we give it good data and good instructions.

### What is intelligence?

- Intelligence is not the opposite of ignorance (knowing it all), if so then encyclopedia was intellegent -> Intelligence doesn’t consist of knowledge alone. You must also be able to use what you know.

- Intelligence is not the ability to answer difficult questions, if so then calculator was intelligent.

- Humans are able to
  - reason by relying on their past experiences
  - make decisions in situations that would be impossible to describe enough for a computer
  - learn new skills
  - use examples to form new concepts
  - create new ideas and imagine new tools
  - communicate by using words, constructing sentences, and putting symbols together to exchange complex, often abstract, notions

- The Turing Test (1950) -> a method for evaluating machine intelligence but chinese room experiment shows the limitation of this test -> the Turing test cannot measure a machine’s intelligence, only its ability to process symbols like a human

- The error is to believe that we can judge a machine’s intelligence by comparing its behavior to a human’s. Turing only wanted to know if we could build a machine capable of thinking. This is why he proposed comparing a machine’s behavior with a human’s.

- To explain this difference, computer scientists Stuart Russell and Peter Norvig, known in universities around the world for their book Artificial Intelligence, offer an amusing analogy with airplanes. Aeronautical engineers build planes according to aerodynamics. They do not try to make machines that fly exactly as pigeons so that they can fool other pigeons.

- The strength of computers is their ability to process large amounts of data very quickly. Whereas a human relies on reasoning or on experience, a machine can instantly test billions of solutions, from the most absurd to the most relevant, or search through gigantic databases.

- Edsger Dijkstra: “The question of whether machines can think is about as relevant as the question of whether submarines can swim.” We build machines that do not think. In some ways, however, they give us the impression they are intelligent. They are not.

### Limitations of Computers

- no general technique for making AI, there are many different methods and algo but they all have sth in common: all designed to overcome two primary computer limitations:
  - memory
  - processing capacity

### Computer Operations

- Complexity:
  - complexity of algo: number of operations necessary for the algorithm to resolve the problem in question based on the input data amount -> depends on the size of the problem

  - complexity of problem: minimum number of operations needed to resolve the problem with a computer (theoretical complexity) -> complexity of the fastest algorithm capable of resolving the problem

- AI is trying to solve the problems that computer can't solve it perfectly because of its limitation (number of ops needed to solve this problem is way higher that the computing power) like playing chess, recognizing a face, preparing a schedule, translating a statement into a foreign language, driving a car -> their algo is not always right but work in a reasonable time

- Very often, making AI consists of developing programs that give us a not-so-bad solution in a reasonable amount of time, when we know the right solution is simply not obtainable.
