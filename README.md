# Lab 3: Asymptotic Analysis

This lab focuses on understanding and analyzing the asymptotic behavior of algorithms. We will explore concepts such as Big-O, Big-$\Theta$, and Big-$\Omega$ notations, and apply them to various algorithmic problems to determine their efficiency and scalability.

**Instructions:** To complete this lab, you may work in groups, but you must write your solutions yourself. Once you have completed the lab, push your changes to your forked repository.

## Problem 1

Suppose $T(n)$ is the worst case running time of an algorithm with input size $n$, and we know that $T(n)$ is $\mathcal{O}(n^3)$ and $\Omega(n^2)$. For each of the following statements, determine whether it must be true, must be false, or could be either true or false. Give a brief justification for each. 

1. $T(n)$ is $\mathcal{O}(n^2)$.

    This statement can be either true or false. We know that $T(n)$ is $\Omega(n^2)$, which means that $T(n)\geq cn^2$ This could mean that $T(n)=cn^2$. If this is true then $T(n)\leq cn^2$, meaning that $T(n) would be $O(n^2)$.

2. $T(n)$ is $\Theta(n^3)$.

    This statement can be either true or false. We know that $T(n)$ is $\Omega(n^2)$, so $T(n)\geq cn^2$ and $T(n)$ is $O(n^3)$, so $T(n)\leq cn^3$. It's possible then that $T(n)\geq cn^3$ since $cn^3> cn^2$ due to its higher polynomial degree. This would mean that $T(n)$ is $\Omega(n^3)$, making it also $\Theta(n^3)$.

3. $T(n)$ is $\Omega(n)$.

    This statement must be true. $cn^2>cn$ since quadratic functions grow faster than linear functions, but since $T(n)\geq cn^2$, then $T(n)\geq cn$. Therefore $T(n)$ is $\Omega(n)$.

4. $T(n)$ is $\Theta(n^{1.5})$.

    This statement must be false. We know that $T(n)\geq cn^2$. Therefore $T(n)\nleq cn^{1.5}$, since $n^2>n^{1.5}$ due to its higher polynomial degree. Therefore $T(n)$ cannot be $O(n^{1.5})$, and thus cannot be $\Theta(n^{1.5})$.

5. $T(n)$ is $\mathcal{O}(n)$.

    This statemnet must be false. We know that $T(n)\geq cn^2$. Therefore $T(n)\nleq cn$, as $n^2>n$ since quadratic functions grow faster than linear functions. Therefore, $T(n)$ cannot be $O(n)$

6. $T(n)$ is $\Theta(n^2 \log n)$.

    This statement could be true or false. By the rule of multiplication, $\Omega(n^2)=\Omega(n^2)\cdot\Omega(1)$, $\Theta(n^2 \log n)=\Theta({n^2})\cdot\Theta(\log n)$, and $O(n^3)=O(n^2)\cdot O(n)$. Since $n>\log n>1$, we can multiply the all terms of the inequality by $n^2$ to get $n^3>n^2 \log n>n^2$. Since $T(n)$ is $O(n^3)$ and $\Omega(n^2)$, $cn^3\geq T(n)\geq n^2$. So, it is possible that $T(n)=c(n^2 \log n)$, meaning that $T(n)$ is $\Theta(n^2 \log n)$.


## Problem 2
Consider the following algorithm where $f(A, i, j)$ is an unknown algorithm that takes as input an array $A$ and two indicies $i$ and $j$ and returns a number. 

```
Mystery Algorithm
Input: An array of int $A$ of length $n$.
Output: int sum
    n = |A|
    sum = 0
    for i = 1 to n:
        for j = 1 to n:
            sum += f(A, i, j)
```

Without knowing anything about $f$, what can we say about the running time of the Mystery Algorithm in terms of $n$? Justify your answer. 

We don't know what the runtime of $f(A,i,j)$ is. Let's say that $f(A,i,j)$ takes $g(n)$ steps. Then, within the most nested for loop, our mystery function takes $3 + g(n)$ steps:

    1 - calling sum initially 
    2 - adding f(A,i,j) to sum 
    3 - assigning a new value to sum 
    + g(n) - the number of steps that $f(A,i,j)$ takes

The two nested for loops themselves means this process is repeated $n^2$ times. Additionally, finding $|A|$ and setting sum=0 account for 2 additional steps at the beginning of our Mystery Algorithm. This means that the runtime of our Mystery Algorithm is given by $T(n)=(3+g(n))n^2+2$. Since we don't know what $g(n)$ is, we cannot say anything about the upper bound runtime for our Mystery algorithm. However we know that $g(n)$ is at least constant. Thus $T(n)\geq(3+c)n^2+2$. Therefore, $\Omega(n^2)$ is a lower bound runtime for $T(n)$.