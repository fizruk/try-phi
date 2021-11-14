<img src="https://www.yegor256.com/images/books/elegant-objects/cactus.svg" height="100px" />

Try [𝜑-calculus](https://www.eolang.org) online: [click here](https://polystat.github.io/try-phi/).

![Demo](images/demo.gif)

Try out these live examples:

1. [Factorial](https://polystat.github.io/try-phi/?snippet=%5B+factorial+-%3E%0A++%5B+n+-%3E+%3F%0A++%2C+%40+-%3E+n.less%28_1+-%3E+2%29.if%28_1+-%3E+1%29%28_2+-%3E%0A++++++n.mul%28_1+-%3E+factorial%28n+-%3E+n.sub%28_1+-%3E+1%29%29%29%0A++++%29%0A++%5D%0A%5D.factorial%28n+-%3E+10%29)
2. [Factorial with user-defined fixpoint combinator](https://polystat.github.io/try-phi/?snippet=%5B+fix+-%3E%0A++%5B+f+-%3E+%3F%0A++%2C+%40+-%3E+f%28x+-%3E+fix%28f+-%3E+f%29%29%0A++%5D%0A%5D.fix%28f+-%3E+%5Bx+-%3E+%3F%2C+n+-%3E+%3F%2C%0A++%40+-%3E+n.less%28_1+-%3E+2%29.if%28_1+-%3E+1%29%28%0A++++_2+-%3E+n.mul%28_1+-%3E+x%28n+-%3E+n.sub%28_1+-%3E+1%29%29%29%0A++%29%0A%5D%29%28n+-%3E+5%29)
3. [Fibonacci numbers](https://polystat.github.io/try-phi/?snippet=%5B+fib+-%3E%0A++%5B+n+-%3E+%3F%0A++%2C+%40+-%3E+n.less%28_1+-%3E+2%29.if%28%0A++++++_1+-%3E+n%0A++++%29%28%0A++++++_2+-%3E+fib%28n+-%3E+n.sub%28_1+-%3E+1%29%29.add%28_1+-%3E+fib%28n+-%3E+n.sub%28_1+-%3E+2%29%29%29%0A++++%29%0A++%5D%0A%5D.fib%28n+-%3E+7%29)

This is an experimental interpreter for a variant of 𝜑-calculus.
Right now we implement it as a term rewriting system with the following features (see [formal rules](images/untyped-calculus-rules.png)):

1. We support the following syntax:

    1. Objects: `[x -> y, y -> [z -> ?]]` (here `?` stands for free attribute marker `ø`)
    2. Attributes: `[y -> x].y.z`
    3. Single named application: `[x -> ?, @ -> x](x -> y)` (`@` stand for 𝜑 attribute)

2. By default, the interpreter will try to immediately parse and dataize an expression written in the editor.

3. If dataization fails, it will nevertheless show original term and its weak head normal form (after last reduction step).

4. At the moment, infinite recursion can hang the page and editor, — simply reload the page!

## How to contribute

* Install and open VS Code
* IDE will ask if you want to clone a repository. Paste URL to this repo
* Open terminal (`Ctrl+` `)
* Install [stack](https://docs.haskellstack.org/en/stable/install_and_upgrade/)
* Build project and make stack rebuild it on changes
    ```sh
    stack build --watch-all
    ```
* Install `Haskell` extension. It will enable linter and documentation on hover
* Open `app/Main.hs` and hover onto a function and check if docs appear
* Run this project
    ```sh
    stack exec try-phi
    ```
* Open in browser http://localhost:8080/