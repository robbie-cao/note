# `grep`

## OR, AND and NOT Operators

### OR

```
grep 'pattern1\|pattern2' filename
grep -E 'pattern1|pattern2' filename
grep -e pattern1 -e pattern2 filename
egrep 'pattern1|pattern2' filename
```

### AND

```
grep -E 'pattern1.*pattern2' filename
grep -E 'pattern1.*pattern2|pattern2.*pattern1' filename
grep -E 'pattern1' filename | grep -E 'pattern2'
```

### NOT

```
grep -v 'pattern1' filename
```

## Advanced Topics

> http://caspar.bgsu.edu/~courses/Stats/Labs/Handouts/grepadvanced.htm

> http://www.thegeekstuff.com/2011/01/advanced-regular-expressions-in-grep-command-with-10-examples-–-part-ii/?-part-ii/

## Reference

- http://www.thegeekstuff.com/2011/10/grep-or-and-not-operators/
