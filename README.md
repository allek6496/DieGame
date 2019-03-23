# DieGame
To find the best solution to a math problem in my math class, the problem is as follows:

You enter a competition where you create fair 6 sided dice, with a catch. You can place exactly 18 pips in any configuration on
the surface of the die, without fractional or negative numbers. Your goal is to design a die that can beat another die with 
faces of [4, 4, 4, 3, 3, 0] at least 50% of the time. Ties are resolved by re-rolling.

However, I didn't want to find just any die, I wanted the best one. So, I made this program.

The program works like this (also see comments for more detailed explaination):
  I start out by creating a class to store and increment the die faces, storing it in a base 6 number and simply adding one to 
  make the next die.
  
  I then loop through each possible die checking if it's better than the last best. If the new best is found, store it as 
  the new best.
  
  However, the tricky part is finding out how likely any particular die is to beat another, and this requires some math.
  
We start out by counting the number of cases where there's a win. For each face on the die you're checking, how many 
faces on the other die can it beat? Just add up each of these numbers to find the number of win cases.

While you're looping through each face, you can also be checking for ties. Ties are whenever the two faces are equal.

Now that we have the number of win and tie cases (and therefore also loss cases because there are only 6*6 = 36 total cases)
we can start to construct the probability of winning.

Let P(Victory) equal the total chance of success
Let P(W) equal the chance of a winning roll
Let P(T) equal the chance of a tie roll

P(Victory) = P(W) + P(T)

The probability of winning is the chance of a winning roll, plus the chance of a tie. Simple, right?

But here's where it gets complicated; whenever you tie, you re-roll the die, resulting in the calculation all over again. This
is shown by multiplying the probability of a tie by the probability of a victory.

P(Victory) = P(W) + P(T)*P(Victory)

However, we know what P(Victory) is! It's just P(W) + P(T)*P(Victory). Substituting this in, we get:

P(Victory) = P(W) + P(T)*[P(W) + P(T)*P(Victory)]
P(Victory) = P(W) + P(T)*[P(W) + P(T)*[P(W) + P(T)*P(Victory)]]

While this pattern goes on forever, this is enough. Expanding this out, a pattern emerges.

P(Victory) = P(W) + P(T)*P(W) + P(T)*P(T)*P(W) + P(T)*P(T)*P(T)*P(Victory)
P(Victory) = P(W) + P(W)*P(T)^1 + P(W)*P(T)^2 + P(W)*P(T)^3*P(Victory)

This is just a geometric sequence! The sum of these is just equal to:

P(Victory) = P(W)*(1/[1-P(T)])

Because there are 36 total cases, and P(W) and P(T) are both fractions with a denominator of 36, this can be simplified.

Let w equal the number of win cases
Let t equal the number of tie cases

P(Victory) = w/36*(1/[1-t/36])
P(Victory) = w/36*(1/[36/36-t/36])
P(Victory) = w/36*(1/[(36-t)/36])
P(Victory) = w/36*36/(36-t)
P(Victory) = w/(36-t)

And this is the equation used in the program to calculate the chance of victory.
