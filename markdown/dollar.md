# How to apply currency number formatting in GitHub Flavored Markdown?

##Problem
If we wish to write two currency amounts, e.g. `$10 and $20`, it appears wonky ($10 and $20) if we use the above syntax.

##Background
GitHub's math rendering capability uses `MathJax`, an open source, JavaScript-based display engine. It delimits the math expressions using `$`.

Hence when we try to write two currency amounts, it interprets everything between the two `$` signs as a math expression and applies a specific formatting. 

##Solution
To ensure that MathJax's formatting is not applied, use `\$` instead of `$`.

Therefore, the correct syntax is `\$10 and \$20` for the output - \$10 and \$20. 