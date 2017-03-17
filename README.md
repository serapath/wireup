# wireup
run and wire up multiple processes

# cli usage
`x | wireup <g1> ... <gN> [--wireup ...] | y`

## <wireup> details
* <g> = <p1 ... pN>
`x | wireup -p <p1 p2 p3> -s <s1 s2 s3> -p <p1 p2 p3> | y`
* i=wireup.stdin, o=wireup.stdout, e=wireup.stderrm -p=parallel, -s=serial
* -i // by default input is ignored; if set, pipes stdin to flaged processes
* -o // by default all output goes to `y`; if set pipes flagged process output to stdout
* -e // by default all output goes to `y`; if set pipes flagges process errors to stderr
  * if -o is manually set, all non-set output by default goes to dev/null
* pX // by default no params or env vars are set

## examples
```
# x1: echo "hello world"
# x2: tr '[a-zA-Z]' '[A-Za-z]'
# x3: ....
```

```
x | wireup
  -p  <x1 x2 x3 x4 --wireup i:1 1:2 2:3 3:4 >
  -p  <x1 x2 x3 --wireup i:1 1:2 2:3 >
  -s  <x1 x2 x3 --wireup i:1 >
  -s  <x1 x2 x3 --wireup i:1 >
  -p  <x1 x2 x3 --wireup i:1 >
  -s  <x1 x2 x3 --wireup i:1 >
  --wireup
    i:1+3
    1:2
    2:3

    g1.o
    g1.e
    g1.&

    >o
    >e
    >oe
| y

```

# node api usage

```js
var wireup = require('wireup')


```
