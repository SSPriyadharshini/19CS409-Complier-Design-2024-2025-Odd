# Ex. No : 4	
# RECOGNITION OF A VALID VARIABLE WHICH STARTS WITH A LETTER FOLLOWED BY ANY NUMBER OF LETTERS OR DIGITS USING YACC
## Register Number :2122230140156
## Name :Priyadharshini S.S
## Date : 06/11/2024

## AIM   
To write a YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits.

## ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the keywords int, float and double and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with YACC compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter a statement as input and the valid variables are identified as output.

## PROGRAM
## LEX CODE
```
%{
#include "y.tab.h"  // Include the YACC header file for token definitions
%}

%%

"int"           { return INT; }
"float"         { return FLOAT; }
"double"        { return DOUBLE; }
[a-zA-Z][a-zA-Z0-9]* { 
    printf("\nIdentifier is %s", yytext);
    return ID;
}
[ \t\n]+        { /* Ignore whitespace */ }
.               { return yytext[0]; }

%%

int yywrap() {
    return 1;  // Indicate end of input for LEX
}
```
## YACC CODE
```
%{
#include <stdio.h>
#include <stdlib.h>
%}

%token ID INT FLOAT DOUBLE  // Define tokens

%%

D: T L
;

L: L ',' ID
 | ID
;

T: INT
 | FLOAT
 | DOUBLE
;

%%

extern FILE *yyin;  // Declare input file pointer

int main() {
    yyin = fopen("input.txt", "r");  // Open input file
    if (!yyin) {
        fprintf(stderr, "Error opening input file\n");
        return 1;
    }

    yyparse();  // Start parsing
    fclose(yyin);  // Close input file
    return 0;
}

void yyerror(char *s) {
    fprintf(stderr, "Error: %s\n", s);  // Error handling
}

```
## INPUT
```

int x,y
```


## OUTPUT 
![image](https://github.com/user-attachments/assets/5710ff01-e653-4908-ab8e-b7a42516c3d0)

## RESULT
A  YACC program to recognize a valid variable which starts with a letter followed by any number of letters or digits is executed successfully and the output is verified.


