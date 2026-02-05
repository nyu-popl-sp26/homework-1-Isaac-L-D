## Solution to Problem 1

(a)

The use of pi at line 4 is bound at line 3, as that version was bound inside the function and so it is the most recent 
and specific to that scope. The use of pi at line 7, meanwhile, is bound at line 1 as the pi inside the definition of 
the circumference function is out of scope for the area function.

(b)

The use of x at line 3 is bound at line 2's function parameter, and the use of x at both line 6 and line 10 are bound at 
line 5's case statement. Lastly, the x at line 13 
is bound at line 1, since it is outside the function f.

## Solution to Problem 2

(a) Execution trace:

```
pow(2,3)
->if  3 > 0 then 2 * pow(2, 3 - 1) else 1 
->if true then 2 * pow(2, 3 - 1) else 1
->2 * pow(2,3-1)
->2 * pow(2,2)
-> 2* (if 2 > 0 then 2 * pow(2, 2 - 1) else 1)
-> 2* (if true then 2 * pow(2, 2 - 1) else 1)
-> 2* ( 2 * pow(2, 2 - 1))
-> 2* ( 2 * pow(2, 1))
-> 2* ( 2 * (if  1 > 0 then 2 * pow(2, 1 - 1) else 1 ))
-> 2* ( 2 * (if  true then 2 * pow(2, 1 - 1) else 1 ))
->2* ( 2 * ( 2 * pow(2, 1 - 1)))
->2* ( 2 * ( 2 * pow(2, 0)))
->2* ( 2 * ( 2 * (if 0 > 0 then 2 * pow(2, 2 - 1) else 1)))
->2* ( 2 * ( 2 * (if false then 2 * pow(2, 2 - 1) else 1)))
->2* ( 2 * ( 2 * (1)))
->2* ( 2 * (2))
->2* (4)
->8
```

(b) Tail-recursive implementation

```scala
def powTail(x: Int, n: Int): Int =
  def powTailHelper(x: Int, n: Int, acc: int): Int =
    if n > 0 then powTailHelper(x, n - 1, acc * x) else acc
  powTailHelper(x,n,1)
```

Execution trace:

```
powTail(2,3)
->powTailHelper(2,3,1)
->if 3 > 0 then powTailHelper(2, 3 - 1, 1 * 2) else 1
->if true then powTailHelper(2, 3 - 1, 1 * 2) else 1
->powTailHelper(2, 3 - 1, 1 * 2)
->powTailHelper(2, 2, 2)
->if 2 > 0 then powTailHelper(2, 2 - 1, 2 * 2) else 2
->if true then powTailHelper(2, 2 - 1, 2 * 2) else 2
->powTailHelper(2, 2 - 1, 2 * 2)
->powTailHelper(2, 1, 4)
->if 1 > 0 then powTailHelper(2, 1 - 1, 4 * 2) else 4
->if true then powTailHelper(2, 1 - 1, 4 * 2) else 4
->powTailHelper(2, 1 - 1, 4 * 2)
->powTailHelper(2, 0, 8)
->if 0 > 0 then powTailHelper(2, 0 - 1, 8 * 2) else 8
->if false then powTailHelper(2, 0 - 1, 8 * 2) else 8
->8
```