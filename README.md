# Compiler

&emsp;&emsp;在《编译原理》课程的学习下，逐渐的掌握一个编译器的结构、作用和实现方法。同时，希望自己在不断的努力下写出一个简单的C语言编译器。


###主要功能

1. 支持`一元运算符`（++，--，!，-），其中++和--有前缀和后缀两种功能
2. 支持`逻辑运算符`：||和&&
3. 支持`算术运算符`：+，-，*，/，%
4. 支持`关系运算符`：>，>=，<，<=，==，！=
5. 控制流：`for`循环，`while`和`do-while`循环
6. 支持`判断语句`if
7. `赋值`操作及`数组`的部分操作

###上下文无关文法

####一、基本框架



Program -> Type main() Block
Type -> int | float | bool
Block -> { Decls Stmts  }
Decls -> Decls Decl | ε
Decl -> Type Array ;
Array -> Array[ Num ] | Identifier
Stmts -> Stmts Stmt | ε




####二、标识符和常数

Letter -> A | B | C | D | E | F | G | H | I | J | K | L | M | N 
&emsp;&emsp;| O | P | Q | R | S | T | U | V | W | X | Y | Z | a | b
&emsp;&emsp;| c | d | e | f | g | h | i | j | k | l | m | n | o | p
&emsp;&emsp;| q | r | s | t | u | v | w | x | y | z | _
Digit -> 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
Non_digit -> 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9
Num -> Num Digit | Non_digit
Identifier -> Identifier Digit | Identifier Letter | Letter
Bool\_value -> true | false

####三、运算符

Unary\_op -> ! | - | ++ | --
Self\_op -> ++ | --
Logic\_op -> || | &&
Math\_op -> + | - | * | / | %
Judge\_op -> == | != | >= | <= | > | <


####四、语句块框架

Stmt -> Assignment
&emsp;&emsp;| if (Bool) Stmt
&emsp;&emsp;| if (Bool) Stmt else Stmt
&emsp;&emsp;| while (Bool) Stmt
&emsp;&emsp;| do Stmt while (Bool) ;
&emsp;&emsp;| for ( Fora ; Forb ; Forc ) Stmt
&emsp;&emsp;| Break ;
&emsp;&emsp;| Block



Fora -> Assignment | ε
Forb -> Bool | ε
Forc -> Assignment | ε



####五、赋值语句


Numlist -> Numlist,Num | Num
Rightside -> Bool | { Numlist } 
Assignment -> Array = Rightside ; | Array Self\_op ; | Self\_op Array ; 

####六、条件语句

Factor -> (Bool) | Array | Num | Bool\_value
Term -> Unary\_op Factor | Factor Self\_op | Factor
Expr -> Expr Math\_op Term | Term
Rel -> Rel Judge\_op Expr | Expr
Bool -> Bool Logic\_op Rel | Rel
