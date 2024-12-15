As the [[Different Phases of a Compiler|initial phase of a compiler]], the primary role of the lexical analyzer is to process the input characters of the source code, organize them into meaningful lexemes, and generate a corresponding sequence of tokens for each lexeme. These tokens are then forwarded to the parser for syntax analysis. The lexical analyzer often interacts with the [[Symbol Table]] during its operations. When it encounters a lexeme representing an identifier, it inserts the lexeme into the symbol table. Additionally, in some instances, the lexical analyzer retrieves information from the symbol table about the type of identifier to help determine the appropriate token to send to the parser.


![[Figure 3.1.png]]

# Regular Expression (regex)
---
**Regular expressions (regex)** play a crucial role in the **lexical analysis** phase of a compiler by defining the patterns for recognizing various lexemes in the source code. The lexical analyzer uses regex to specify and match the structure of tokens such as keywords, identifiers, operators, literals and delimiters. By leveraging the concise and expressive nature of regex, the lexical analyzer can efficiently distinguish between different token types, ensuring accurate *tokenization* of the input program.

**Constants and compound expressions** are the building blocks of regex.

**Constants**:
- $\emptyset$ : represents an empty language, i.e., empty set.
- Single character `c`: represents a singleton set consisting of just `c` as a member, i.e., a set of 1 element {`c`}.
- Epsilon $\epsilon$: represents a singleton set consisting of just `''`  as a member, i.e., the set of 1 element {''}.

**Compounds**: Given a regex $A$  and $B$, we can apply the following operators over them to obtain another regex:
- Union: $A + B$ or $A || B$:
	- {"ab", "c"} | {"ab", "d", "ef"} = {"ab, "c", "d", "ef"}
- Concatenation: $AB$
	- {"ab", "c"} {"d", "ef"} = {"abd", "abef", "cd", "cef"}
- Iteration: (Kleene star)
    - A∗=⋃i≥0Ai
    - Ai=A…i times A
    - A0=ϵ
    - (0+1)* = {"0", "1"}* = {e, 0, 1, 00, 11, 01, 10, ...} # set of all binary string (including the empty string)
    - {"ab", "c"}* = {e, "ab", "c", "abab", "cc", "abc", "cab", ...}

# Finite Automata

Using **regex** we can describe various languages (e.g., `digits: digit digit*`, `identifier: letter (letter+digit)*`). to implement this, we need a system that takes a regular expression $R$ representing a regular language $L(R)$, along with an input string $s$, 
returning `accept` if $s \in L(R)$ and `reject` otherwise. this can be achieved by using **Finite Automata**

A **Finite Automata** consists of:
- $\Sigma$ : An input alphabet.
- $S$ : A finite set of states.
- $n$ : Start state.
- $F \subseteq S$ : A set of accepting states.
- `state -> input -> state`: A set of transitions.
	- `state -> a -> state`: In state s1 on input `a` go to state s2.
	- If end of input and in accepting state, then `accept`
	- Otherwise, `reject`

>[!note]  $\epsilon$-move
>Automaton can chose to either **stay** or take $\epsilon$-move (move to a different state but **do not** consume an input)


## Deterministic Finite Automata (DFA) vs Non-Deterministic Finite Automata (NFA)

A **Deterministic Finite Automata (DFA)** and a **Non-Deterministic Finite Automata (NFA)** are both mathematical models used to recognize regular languages. A **DFA** is a type of finite automation where for each state and input symbol, there is exactly one transition to a next state. This ensures a single deterministic path of execution for any given input string. In contrast, an **NFA** allows multiple possible transitions from a state for the same input symbol, or even no transition at all ($\epsilon$ moves). While DFAs are simpler and easier to implement due to their deterministic nature, NFAs are more flexible in their design. However, any language that can be recognized by an NFA can also be recognized by a DFA, as both models are equivalent in terms of the languages they can recognize, though NFAs might require fewer states in some cases.

| DFA                                  | NFA                                                                                                                 |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------- |
| One transition per input per state   | Multiple transitions for one input in a given state                                                                 |
| No $\epsilon$-moves                  | Can have $\epsilon$-moves                                                                                           |
| One path through the state graph     | Multiple paths through the state graphs                                                                             |
| Each transition results in one state | A transition can result in a set of states (if any is final at the end of the input, `accept`, Otherwise, `reject`) |
| Faster to execute                    | Slower (exponentially) to execute                                                                                   |
| Exponentially large                  | Exponentially smaller                                                                                               |

## Regular Expression to NFA

A **Lexical Analyzer** performs these conversions internally to decide whether a token is Accepted by the language's specifications and *reports an error* if not. and for every regex we can define an equivalent NFA:

- For $\epsilon$:
![[Pasted image 20241206212313.png]]

- For a:
![[Pasted image 20241206212153.png]]
- For $AB$:
![[Pasted image 20241206212501.png]]

- For $A + B$:
![[Pasted image 20241206214003.png]]

- For $A*$:
![[Pasted image 20241206214100.png]]


## NFA to DFA

After converting a regular expression (RE) to an NFA, the lexer internally transforms the NFA into a DFA. In an NFA with `n` states each state can transition to a maximum of `n` other states. Additionally, there are $2^2 - 1$ possible *non-empty subsets of states or configurations*. As a result, converting an NFA with `n` states can generate a DFA with up to $2^n - 1$ states.

for example if we were to convert the following NFA:

#TODO: Add Graphs to conversion from DFA to NFA



