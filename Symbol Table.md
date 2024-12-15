# Introduction
---
A Symbol Table is a critical data structure in a compiler that stores information about identifiers (such as variable names, function names, constants, etc.) used in a program. It acts as a centralized repository to track each identifier's attributes, such as its name, data type, scope, memory location, and usage. The symbol and maintained during the **Lexical Analysis** and **Syntax Analysis** phases and is used throughout subsequent phases like **Semantic Analysis** and **Code Generation**. By organizing and managing this information efficiently, the symbol table helps the compiler perform tasks like type checking, scope resolution, and memory allocation, ensuring that the program adheres to language rules and is correctly translated into executable code.

## Usage by Phases

- **Lexical Analysis**: Creates entries for identifiers.
- **Syntax Analysis**: Adds information regarding attributes.
- **Semantic Analysis**: Using available info checks *Semantics* & updates the symbol table.
- **Intermediate Code Generation**: Available info helps adding temporary variable's information.
- **Code Optimization**: Information available in the symbol table is used in **Machine Dependent** optimization.
- **Target Code Generation**: Generates the *Target Code* using address information of the identifiers.

# Entries in a Symbol Table
---
The entries of a symbol table represent information about identifiers in a program. Each entry provides details that the compiler uses during various phases to analyze and generate code correctly. The specific attribute stored depend on the type of identifier (e.g., variable, function, or constant).

However, **common entries include:**
1. **Name**: The identifier's name (e.g., variable or function name) serves as the key to look up its information in the table.
2. **Type**: The data type of the identifier, such as `int`, `float`, `char`, or user-defined types (for variables and functions).
3. **Scope**: The region of the program (e.g., global, local, or block-level) where the identifier is valid and accessible.
4. **Memory Location / Address**: The location in memory (stack, heap, or global section) or the offset where the identifier is stored.
5. **Value (if applicable)**: The constant value for literals or the initial value for variables.
6. **Size**: The amount of memory required by the identifier (e.g., 4 bytes for an integer, depending on the platform).
7. **Usage**: Information about how the identifier is used, such as being read-only (e.g., constants) or mutable.
8. **Functions Parameters (if applicable)**: For functions, the list of parameters, their types, and order are stored.
9. **Return Type (for functions)**: The data type of the value returned by a function (e.g., `void`, `int`).
10. **Pointer/Reference Information**: Indicates if the identifier is a pointer or reference, including levels of indirection (e.g., `int*`, `char**`).
11. **Array Dimensions (if applicable)**: For arrays, the number of dimensions and the size of each dimension.
12. **Attributes (for classes or objects)**: For object-oriented languages, it may include class names, member functions, and member variables.
13. **Line of Declaration**: The line number in the source code where the identifier has been declared.
14. **The line of Usage**: The line number where the identifier has been used in the code (If the identifier has been used multiple times throughout the source code, all of those line numbers will be saved in a linked list for every identifier entry).

To enhance clarity, we will simplify our symbol table to include only a few key entries for illustrative purposes. And those will be **Name, Type, Size, Dimension (Array Dimensions), Line of Declaration, Line of Usage, Address**

```c
int count;
char x[] = "HELLO, FRIEND";
```

| Name    | Type   | Size | Dimension | Line of Declaration | Line of Usage     | Address           |
| ------- | ------ | ---- | --------- | ------------------- | ----------------- | ----------------- |
| `count` | `int`  | 2    | 0         | ==blank for now==   | ==blank for now== | ==blank for now== |
| `x`     | `char` | 13   | 1         | --                  | --                | --                |

# Operations
---
A symbol table is a dynamic structure that supports various operations during the compilation process to **store, retrieve and manage information about identifiers**. The key operations performed on a symbol table include:

1. **Insertion**: Add a new entry for an identifier into the symbol table.
2. **Lookup**: Retrieve information about an identifier by search the table using its name.
3. **Update**: Modify the attributes of an existing entry in the table.
4. **Deletion**: Remove an identifier from the symbol table.
5. **Scope Management**: Handle entries for identifiers in nested or block-specific scopes.
6. **Traversal**: Iterate through all entries in the table for purposes such as optimization or code generation.

>[!note] Note
>This approach is used in modern **block-structured languages** (i.e., C, Java, Python) that use a hierarchical scoping mechanism, allowing variables to be declared within nested blocks such as functions, loops, or conditionals. However in older **non-block structured languages** (i.e., early versions of **BASIC**), identifiers had a *global scope*, meaning they are accessible throughout the entire program.

