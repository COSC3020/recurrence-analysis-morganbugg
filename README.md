[![Open in Visual Studio Code](https://classroom.github.com/assets/open-in-vscode-718a45dd9cf7e7f842a935f5ebbe5719a5e09af4491e668f4dbf3b35d5cca122.svg)](https://classroom.github.com/online_ide?assignment_repo_id=12116529&assignment_repo_type=AssignmentRepo)
# Recurrence Analysis -- Mystery Function

Analyze the running time of the following recursive procedure as a function of
$n$ and find a tight big $O$ bound on the runtime for the function. You may
assume that each operation takes unit time. You do not need to provide a formal
proof, but you should show your work: at a minimum, show the recurrence relation
you derive for the runtime of the code, and then how you solved the recurrence
relation.

```javascript
function mystery(n) {
    if(n <= 1)
        return;
    else {
        mystery(n / 3);
        var count = 0;
        mystery(n / 3);
        for(var i = 0; i < n*n; i++) {
            for(var j = 0; j < n; j++) {
                for(var k = 0; k < n*n; k++) {
                    count = count + 1;
                }
            }
        }
        mystery(n / 3);
    }
}
```

Add your answer to this markdown file. [This
page](https://docs.github.com/en/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)
might help with the notation for mathematical expressions.

---

### Answer

First, we can deconstruct the function into the following recurrence relation: </br>

$1$ if $n \leq 1$ </br>
$3T(\frac{n}{3}) + n^5$ else </br>

To determine the complexity, we can do the following: </br>

$T(n) = 3T(\frac{n}{3}) + n^5$ </br>

We'll start by looking at an iteration of this to try and establish a pattern. </br>

$= 3(3T(\frac{\frac{n}{3}}{3}) + (\frac{n}{3})^5) + n^5$ </br>
$= 9T(\frac{n}{3}) + \frac{3n^5}{3^5} + n^5$ </br>

We can separate $n^5$ from the fraction here to separate our terms and make it clearer what it is we're dealing with at this point. </br>

$= 9T(\frac{n}{3}) + \frac{3}{3^5} \cdot n^5 + n^5$ </br>

From here, we can determine a sum as follows from the latter half of this expression. </br>
$= 3^iT(\frac{n}{3^i}) + \displaystyle\sum_{j=0}^{i-1}\frac{3^j}{(3^j)^5} \cdot n^5$ </br>
At this point, we want to substitute for a value of $i$, so we will use $i = \log_3(n)$. </br>
$= 3^{\log_3(n)}T(\frac{n}{3^{\log_3(n)}}) + \displaystyle\sum_{j=0}^{\log_3(n)-1}\frac{3^j}{(3^j)^5} \cdot n^5$ </br>
We can now simplify the first half of this expression, and our sum can be simplified as follows, where $k$ is a constant: </br>
$= n + \displaystyle\sum_{j=0}^{\log_3(n)-1}k \cdot n^5$ </br>
From this sum, we can determine that there are a logarithmic number of elements mutliplied by $n^5$, therefore we know that $T(n) \in \Theta(n^5 \cdot \log_3(n))$

<!-- While this is largely based off of our discussion in class, I did my best to display comprehension through my explanations throughout -->