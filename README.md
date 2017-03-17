# wireup
run and wire up multiple processes

# usage
`x | <wireup> | y`

## <wireup>
1. `wireup <g1> ... <gN>`
2. should pipe content to FLAGGED in
3. should pipe from FLAGGED out

## <g>
* <g serial>
* <g parallel>

## details
`x | wireup -p <p1 p2 p3> -s <s1 s2 s3> -p <p1 p2 p3> | y`
* -i // by default input is ignored
* -o // by default all output goes to `y`
* pX // by default no params or env vars are set

```
# p1: echo aSdF
# p2: tr '[a-zA-Z]' '[A-Za-z]'
```

`x | wireup -p <p1 p2 p3> -s <s1 s2 s3> -p <p1 p2 p3> --wireup i: | y`

# inspiration
0 === input
1>>TARGET
1>TARGET
2>>TARGET
2>TARGET

&>>TARGET
&>TARGET
------------------------------------------------------
1 >  filename   # Redirect stdout to file "filename."
1 >> filename   # Redirect and append stdout to file "filename."
2 >  filename   # Redirect stderr to file "filename."
2 >> filename   # Redirect and append stderr to file "filename."
&>   filename   # Redirect both stdout and stderr to file "filename."
M > N   # "M" is a file descriptor, which defaults to 1, if not explicitly set.
            # "N" is a filename.
            # File descriptor "M" is redirect to file "N."
M > &N  # "M" is a file descriptor, which defaults to 1, if not set.
            # "N" is another file descriptor.
