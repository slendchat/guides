### File Descriptors (FD)
- `0` = **stdin** (input)
- `1` = **stdout** (standard output)
- `2` = **stderr** (standard error)

### Basic Redirection

1. stdout (1) → file
```
command > file
# or
command 1> file
```

2. stderr (2) → file
```
command 2> error.log 
```

3. stdout + stderr → one file
```
command > all.log 2>&1
```
- `> all.log`: redirect **stdout (1)** to `all.log`
- `2>&1`: redirect **stderr (2)** to where stdout (1) is go

4. Append instead of overwrite
```
command >> out.log       # stdout append
command 2>> error.log    # stderr append
```

5. Redirect stdin
```
command < input.txt
# for example:
cat < input.txt
```
