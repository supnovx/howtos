
# cat

```
$ cat [OPTION]... [FILE]...
# Concatenate FILE(s), or standard input, to standard output.
# With no FILE, or when FILE is -, read standard input.

-b, --number-nonblank     number nonempty output lines, override -n
-n, --number              number all output lines
```

## Output from input
```
$ cat
input line one # standard input
input line one
input line two # standard input
input line two

# Multiple input lines util reach "EOF"
$ cat << EOF
> input line one # standard input
> input line two # standard input
> EOF            # standard input
input line one
input line two
```

## Output from files
```
$ cat a.txt b.txt
file a content
file b content
```

## Output from files and standard input
```
$ cat a.txt - b.txt << EOF
> input line one
> input line two
> EOF
file a content
input line one
input line two
file b content

# when with multiple (-), only the first one is valid
$ cat a.txt - b.txt - a.txt - b.txt << EOF
> input line one
> input line two
> EOF
file a content
input line one
input line two
file b content
file a content
file b content
```

## Redirect standard output to file

(1) Standard Input => Standard Output => File
```
# Truncate the file (create a new one if isn't exist) and output to the file
$ cat << EOF > c.txt
> input line one for c.txt
> input line two for c.txt
> EOF
$ cat c.txt
input line one for c.txt
input line two for c.txt

# Append to a file (creat a new one if isn't exist)
$ cat << EOF >> c.txt
> input line three for c.txt
> EOF
$ cat c.txt
input line one for c.txt
input line two for c.txt
input line three for c.txt

$ cat << EOF > c.txt
> input line one for c.txt truncate
> EOF
$ cat c.txt
input line one for c.txt truncate

```

(2) Files => Standard Output => File
```
$ cat a.txt b.txt > c.txt
$ cat c.txt
file a content
file b content

$ cat a.txt b.txt >> c.txt
$ cat c.txt
file a content
file b content
file a content
file b content
```

(3) Files and Standard Input => Standard Output => File
```
$ cat a.txt - b.txt << EOF > c.txt
> input line one for c.txt
> input line two for c.txt
> EOF
$ cat c.txt
file a content
input line one for c.txt
input line two for c.txt
file b content

$ cat - b.txt << EOF >> c.txt
> input line three for c.txt
> EOF
$ cat c.txt
file a content
input line one for c.txt
input line two for c.txt
file b content
input line three for c.txt
file b content
```

## Output with line numbered
```
$ cat << EOF > c.txt
> input line for c.txt
> input line for c.txt
>
> input line for c.txt
> EOF
$ cat -b c.txt # only number non-empty lines
     1  input line for c.txt
     2  input line for c.txt

     3  input line for c.txt
$ cat -n c.txt # number all lines
     1  input line for c.txt
     2  input line for c.txt
     3
     4  input line for c.txt

$ cat -b c.txt c.txt > d.txt
$ cat d.txt
     1  input line for c.txt
     2  input line for c.txt

     3  input line for c.txt
     4  input line for c.txt
     5  input line for c.txt

     6  input line for c.txt
     
$ cat -n c.txt c.txt > d.txt
$ cat d.txt
     1  input line for c.txt
     2  input line for c.txt
     3
     4  input line for c.txt
     5  input line for c.txt
     6  input line for c.txt
     7
     8  input line for c.txt
```

## Output from last line to first line
```
$ tac << EOF
> input line 1
> input line 2
> input line 3
> EOF
input line 3
input line 2
input line 1
```
