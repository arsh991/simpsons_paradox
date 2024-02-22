The below algorithm describes the numerical search we deploy for finding causes. We use the *Mathematica* software for the numerical calculations. Note, that the function that is being maximized in the algorithm is degenerate and has many maxima for a given input $p(a_1, a_2, b)$. Thus, one needs a method to cover these maxima. We use  **FindMaximum**  function available in  *Mathematica*  software which 
enables the specification of initial points for the variables under consideration. By randomly selecting these initial points, diverse maximum points for the given $p(a_1, a_2, b)$ are obtained.
The condition written in the pseudocode is for generating causes that support aggregation. The condition should be changed correspondingly to get the other options. 

## Algorithm: Searching for a cause supporting aggregation

1. $i \gets 0$ and $j \gets 0$.
   
2. **For** $i \leq N$:                                     
      - **Do**
          - From uniform distribution independently sample conditional probabilities $p(a_1|a_2, b)$, $p(a_1|\bar{a}_2, b)$, $p(a_1|a_2, \bar{b})$, $p(a_1|\bar{a}_2, \bar{b})$.
      - **While** $p(a_1 | a_2, b) \leq p(a_1 | \bar{a}_2, b)$ and $p(a_1|a_2, \bar{b}) \leq p(a_1|\bar{a}_2, \bar{b})$.
      
      - From uniform distribution sample $p(a_2)$.
      - **Do**
          - From uniform distribution independently sample conditional probabilities $p(b|a_2)$, $p(b|\bar{a}_2)$.
      - **While** $p(a_1 | a_2) \geq p(a_1 | \bar{a}_2)$.
      
      - **For** $j \leq M$: 
          - For random initial conditions, find:
            $\underset{p(a_1, a_2, c), p(b|c)}{\arg \max} {-\alpha \sum_{a_1, a_2, b} [\sum_c p(a_1,a_2, c)p(b|c)-p(a_1,a_2,b)]^2 }$ (We set $\alpha$ to 10000).
          
          - **If** $p(a_1| a_2, c_1) <  p(a_1| \bar{a}_2, c_1)$ and $p(a_1| a_2, c_2) <  p(a_1| \bar{a}_2, c_2)$ and $p(a_1| a_2, c_3) <  p(a_1| \bar{a}_2, c_3)$: 
              - **Print** $p(a_1, a_2, b, c)$.
      
          -  $j \gets j + 1$ 
      
   -  $i \gets i+1$ 
