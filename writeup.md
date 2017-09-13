# Lab 6 Written Problems
# Scala Basics: Binding and Scope
### Written by Brennon Lee (ID: 103419905) and D'Artagnan Wake (ID: ########)

**3.**
**Part B.**

**(I.)**  Exercise. In your write-up, give a refactored version of the regrammar from ?? that eliminates ambiguity in BNF (not EBNF).
    Use the following template for the new non-terminal names:

**ANS:**

         re ::= union
         union ::= union '|' intersect | intersect
         intersect ::= intersect '&' concat | concat
         concat ::= concatnot | not
         not ::= '~' not | star
         star ::= star'*' | star'?' | star'+' | atom
         atom ::= c | '#' | '!' | '.' |


**(II.)** Exercise. Explain briefly why a recursive descent parser following your grammar with left recursion would go into an infinite loop.

**ANS:**

       If the right side does not match on anything and because the grammar is left recursive  
       the left side will get stuck in an infinite loop not being able to match on anything.

**(III.)**  Exercise. In your write-up, give a refactored version of the re grammar that re- places left-associative binary operators with n-ary versions using EBNF using the following template:

   **ANS:**    

         re ::= union
         union ::= intersect { ‘|’ intersect }
         intersect ::= concat { '&' concat }
         concat ::=  not { concatnot }
         not ::= star { '*'star }
         star ::= atom { '*' atom | '+' atom | '?' atom }
         atom ::=  '!' | '#' | '.' | c | '('re')' | atom





**(IV.)** In your write-up, give the full refactored grammar in BNF without left recursion and new non-terminals like unions for lists of symbols. You will need to introduce new terminals for intersects and so forth.

**ANS:**

            re ::= union

            union ::= intersect unions
            unions ::= epsilon | '|' intersect unions

            intersect ::= concat intersects
            intersects ::= epsilon | '&' concat intersects

            concat ::= not concats
            concats ::= epsilon | notconcats

            not ::= star | '~' not

            star ::= atom stars
            stars ::= epsilon | '*' atom stars

            atom ::= 'c' | '#' | '!' | '.' | '('re')'






 **Part C.**

 **I.** In your write-up, give typing and small-step operational semantic rules for regular expression literals and regular expression tests based on the informal specification given above. Clearly and concisely explain how your rules enforce the constraints given above and any additional decisions you made.

 **ANS:**

            Type Regex    


            ----------------------
              T ⊢ /^re$/: RegExp


            Type tests


             T ⊢ e1: RegExp  T ⊢ e2: String
            ---------------------------------
                  e1.test(e2): Bool


            Search Test 1


                        e1 -> e1'
            -------------------------------
              e1.test(e2) -> e1'.test(e2)


            Search Test 2


                          e2 -> e2'
            -------------------------------------
             /^re$/.test(e2) -> /^re$/.test(e2')


            Do Test


                  S ∈ /^re$/
            ------------------------
             /^re$/.test(S) -> True
