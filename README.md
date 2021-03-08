# Awesome-Grammar-Fuzzing
This list aims at helping you to do your research / develop toward Grammar based fuzzing. This includes the latest research papers, projects, blogs and tutorials. 


# Academic Papers
- [Input Algebras](https://publications.cispa.saarland/3208/7/gopinath2021input.pdf)
    - Grammar-based test generators are highly efficient in producing syntactically valid test inputs, and give their user precise control over which test inputs should be generated. Adapting a grammar or a test generator towards a particular testing goal can be tedious, though. We introduce the concept of a grammar transformer, specializing a grammar towards inclusion or exclusion of specific patterns: “The phone number must not start with 011 or +1”. To the best of our knowledge, ours is the first approach to allow for arbitrary Boolean combinations of patterns, giving testers unprecedented flexibility in creating targeted software tests. The resulting specialized grammars can be used with any grammar-based fuzzer for targeted test generation, but also as validators to check whether the given specialization is met or not, opening up additional usage scenarios. In our evaluation on real-world bugs, we show that specialized grammars are accurate both in producing and validating targeted inputs.
    
- [Growing A Test Corpus with Bonsai Fuzzing](https://rohan.padhye.org/files/bonsai-icse21.pdf) (ICSE'21)
    - This paper presents a coverage-guided grammar-based fuzzing technique for automatically generating a corpus of concise test inputs for programs such as compilers. We walk-through a case study of a compiler designed for education and the corresponding problem of generating meaningful test cases to provide to students. The prior state-of-the-art solution is a combination of fuzzing and test-case reduction techniques such as variants of delta-debugging. Our key insight is that instead of attempting to minimize convoluted fuzzer-generated test inputs, we can instead grow concise test inputs by construction using a form of iterative deepening. We call this approach Bonsai Fuzzing. Experimental results show that Bonsai Fuzzing can generate test corpora having inputs that are 16–45% smaller in size on average as compared to a fuzz-then-reduce approach, while achieving approximately the same code coverage and fault-detection capability.    

- [Toward Automated Grammar Extraction via Semantic Labeling of Parser Implementations](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9283881) (SPW'20)
    - This paper introduces a new approach for labeling the semantic purpose of the functions in a parser. An input file with a known syntax tree is passed to a copy of the target parser that has been instrumented for universal taint tracking. A novel algorithm is used to merge that syntax tree ground truth with the observed taint and control-flow information from the parser's execution, producing a mapping from types in the file format to the set of functions most specialized in operating on that type. The resulting mapping has applications in mutational fuzzing, reverse engineering, differential analysis, as well as automated grammar extraction. We demonstrate that even a single execution of an instrumented parser with a single input file can lead to a mapping that a human would identify as intuitively correct.

- [Inputs from Hell Learning Input Distributions for Grammar-Based Test Generation](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9154602)
    - Grammars can serve as producers for structured test inputs that are syntactically correct by construction. A probabilistic grammar assigns probabilities to individual productions, thus controlling the distribution of input elements. Using the grammars as input parsers, we show how to learn input distributions from input samples, allowing to create inputs that are similar to the sample; by inverting the probabilities, we can create inputs that are dissimilar to the sample. This allows for three test generation strategies: 1) “Common inputs” – by learning from common inputs, we can create inputs that are similar to the sample; this is useful for regression testing. 2) “Uncommon inputs” – learning from common inputs and inverting probabilities yields inputs that are strongly dissimilar to the sample; this is useful for completing a test suite with “inputs from hell” that test uncommon features, yet are syntactically valid. 3) “Failure-inducing inputs” – learning from inputs that caused failures in the past gives us inputs that share similar features and thus also have a high chance of triggering bugs; this is useful for testing the completeness of fixes. Our evaluation on three common input formats (JSON, JavaScript, CSS) shows the effectiveness of these approaches. Results show that “common inputs” reproduced 96% of the methods induced by the samples. In contrast, for almost all subjects (95%), the “uncommon inputs” covered significantly different methods from the samples. Learning from failure-inducing samples reproduced all exceptions (100%) triggered by the failure-inducing samples and discovered new exceptions not found in any of the samples learned from. 

    
- [Abstracting failure-inducing inputs](https://rahul.gopinath.org/resources/issta2020/gopinath2020abstracting.pdf) (ISSTA'20)
    -  A program fails. Under which circumstances does the failure occur? Starting with a single failure-inducing input “The input ‘((4))’ fails”) and an input grammar, the DDSET algorithm uses systematic tests to automatically generalize the input to an abstract failure-inducing input that contains both (concrete) terminal symbols and (abstract) nonterminal symbols from the grammar - for instance, “((<expr>))”, which represents any expression in double parentheses. Such an abstract failure-inducing input can be used as a debugging diagnostic, characterizing the circumstances under which a failure occurs (“The error occurs whenever an expression is enclosed in double parentheses”); as a producer of additional failure-inducing tests to help design and validate fixes and repair candidates (“The inputs ‘((1))’, ‘((3 * 4))’, and many more also fail”). In its evaluation on real-world bugs in JavaScript, Clojure, Lua, and Coreutils, DDSET’s abstract failure-inducing inputs provided to-the-point diagnostics, and precise producers.
    
- [Building Fast Fuzzers](https://arxiv.org/pdf/1911.07707.pdf)
    - In this paper, we describe how to build fast grammar fuzzers from the ground up, treating the problem of fuzzing from a programming language implementation perspective. Starting with a Python textbook approach, we adopt and adapt optimization techniques from functional programming and virtual machine implementation techniques together with other novel domain-specific optimizations in a step-by-step fashion. In our F1 prototype fuzzer, these improve production speed by a factor of 100--300 over the fastest grammar fuzzer Dharma. As F1 is even 5--8 times faster than a lexical random fuzzer, we can find bugs faster and test with much larger valid inputs than previously possible.   

- [NAUTILUS: Fishing for Deep Bugs with Grammars](https://www.syssec.ruhr-uni-bochum.de/media/emma/veroeffentlichungen/2018/12/17/NDSS19-Nautilus.pdf) (NDSS'19)
    - In this paper, we propose NAUTILUS, a method to efficiently fuzz programs that require highly-structured inputs by combining the use of grammars with the use of code coverage feedback. This allows us to recombine aspects of interesting inputs that were learned individually, and to dramatically increase the probability that any generated input will be accepted by the parser. We implemented a proof-of-concept fuzzer that we tested on multiple targets, including ChakraCore (the JavaScript engine of Microsoft Edge), PHP, mruby, and Lua. NAUTILUS identified multiple bugs in all of the targets: Seven in mruby, three in PHP, two in ChakraCore, and one in Lua. Reporting these bugs was awarded with a sum of 2600 USD and 6 CVEs were assigned. Our experiments show that combining context-free grammars and feedback-driven fuzzing significantly outperforms state-of-the-art approaches like American Fuzzy Lop (AFL) by an order of magnitude and grammar fuzzers by more than a factor of two when measuring code coverage.

- [Mining input grammars from dynamic control flow](https://dl.acm.org/doi/pdf/10.1145/3368089.3409679)
    - In this paper, we present a general algorithm that takes a program and a small set of sample inputs and automatically infers a readable context-free grammar capturing the input language of the program. We infer the syntactic input structure only by observing access of input characters at different locations of the input parser. This works on all stack based recursive descent input parsers, including parser combinators, and works entirely without program specific heuristics. Our Mimid prototype produced accurate and readable grammars for a variety of evaluation subjects, including complex languages such as JSON, TinyC, and JavaScript.

- [Evolutionary Grammar-Based Fuzzing](https://link.springer.com/chapter/10.1007%2F978-3-030-59762-7_8) (SSBSE ‘20)
    - In this paper, we present EvoGFuzz, an evolutionary grammar-based fuzzing approach to optimize the probabilities to generate test inputs that may be more likely to trigger exceptional behavior. The evaluation shows the effectiveness of EvoGFuzz in detecting defects compared to probabilistic grammar-based fuzzing (baseline). Applied to ten real-world applications with common input formats (JSON, JavaScript, or CSS3), the evaluation shows that EvoGFuzz achieved a significantly larger median line coverage for all subjects by up to 48% compared to the baseline. Moreover, EvoGFuzz managed to expose 11 unique defects, from which five have not been detected by the baseline.

- [Superion: Grammar-Aware Greybox Fuzzing](https://arxiv.org/pdf/1812.01197.pdf) (ICSE'19)
    - we propose a grammar-aware coverage-based greybox fuzzing approach to fuzz programs that process structured inputs. Given the grammar (which is often publicly available) of test inputs, we introduce a grammar-aware trimming strategy to trim test inputs at the tree level using the abstract syntax trees (ASTs) of parsed test inputs. Further, we introduce two grammar-aware mutation strategies (i.e., enhanced dictionary-based mutation and tree-based mutation). Specifically, tree-based mutation works via replacing subtrees using the ASTs of parsed test inputs. Equipped with grammar-awareness, our approach can carry the fuzzing exploration into width and depth.

- [Pythia: Grammar-Based Fuzzing of REST APIs with Coverage-guided Feedback and Learning-based Mutations](https://arxiv.org/pdf/2005.11498.pdf)
    - This paper introduces Pythia, the first fuzzer that augments grammar-based fuzzing with coverage-guided feedback and a learning-based mutation strategy for stateful REST API fuzzing. Pythia uses a statistical model to learn common usage patterns of a target REST API from structurally valid seed inputs. It then generates learning-based mutations by injecting a small amount of noise deviating from common usage patterns while still maintaining syntactic validity. Pythia's mutation strategy helps generate grammatically valid test cases and coverage-guided feedback helps prioritize the test cases that are more likely to find bugs. We present experimental evaluation on three production-scale, open-source cloud services showing that Pythia outperforms prior approaches both in code coverage and new bugs found. Using Pythia, we found 29 new bugs which we are in the process of reporting to the respective service owners.

- [Generating Highly-structured Input Data by Combining Search-based Testing and Grammar-based Fuzzing](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=9286098) (ASE'20)
    - Software testing is an important and time-consuming task that is often done manually. In the last decades, researchers have come up with techniques to generate input data (e.g., fuzzing) and automate the process of generating test cases (e.g., search-based testing). However, these techniques are known to have their own limitations: search-based testing does not generate highly-structured data; grammar-based fuzzing does not generate test case structures. To address these limitations, we combine these two techniques. By applying grammar-based mutations to the input data gathered by the search-based testing algorithm, it allows us to co-evolve both aspects of test case generation. We evaluate our approach, called G-EVOSUITE, by performing an empirical study on 20 Java classes from the three most popular JSON parsers across multiple search budgets. Our results show that the proposed approach on average improves branch coverage for JSON related classes by 15 % (with a maximum increase of 50 %) without negatively impacting other classes.

- [Automatic Generation of Input Grammars Using Symbolic Execution ](https://digitalcommons.dartmouth.edu/cgi/viewcontent.cgi?article=1162&context=senior_theses)
    - Invalid input often leads to unexpected behavior in a program and is behind a plethora of known and unknown vulnerabilities. To prevent improper input from being processed, the input needs to be validated before the rest of the program executes. Formal language theory facilitates the definition and recognition of proper inputs. We focus on the problem of defining valid input after the program has already been written. We construct a parser that infers the structure of inputs which avoid vulnerabilities while existing work focuses on inferring the structure of input the program anticipates. We present a tool that constructs an input language, given the program as input, using symbolic execution on symbolic arguments. This differs from existing work which tracks the execution of concrete inputs to infer a grammar. We test our tool on programs with known vulnerabilities, including programs in the GNU Coreutils library, and we demonstrate how the parser catches known invalid inputs. We conclude that the synthesis of the complete parser cannot be entirely automated due to limitations of symbolic execution tools and issues of computability. A more comprehensive parser must additionally be informed by examples and counterexamples of the input language.
______________________________________
# Blog posts
- Resmack-Rust Grammar Fuzzing (Grammar fuzzing series by James Johnson [@d0c_s4vage](https://twitter.com/d0c_s4vage))
    - [Resmack-rust - Grammar Fuzzing Thoughts (Part 1)](https://narly.me/posts/resmack-grammar-fuzz-thoughts-1/)
    - [Resmack-rust - Full Fuzzer Detour (Part 2)](https://narly.me/posts/resmack-detour-full-fuzzer-experiment/)
    - [Resmack-rust - Perf Event Performance Overhead (Part 3)](https://narly.me/posts/resmack-detour-perf-benchmark/)
    - [Resmack-rust - Grammar Mutations (Part 4)](https://narly.me/posts/resmack-grammar-fuzz-thoughts-4/)
    - [Resmack-rust - Grammar Mutation and Recursion (Part 5)](https://narly.me/posts/resmack-grammar-fuzz-thoughts-5/)
    - [Resmack-rust - Stateful & Dynamic Grammars (Part 6)](https://narly.me/posts/resmack-grammar-fuzz-thoughts-6/)
   
- [Fuzzing with Grammars](https://www.fuzzingbook.org/html/Grammars.html) ([FuzzingBook](https://www.fuzzingbook.org/))
