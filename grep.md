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

## Reference

- http://www.thegeekstuff.com/2011/10/grep-or-and-not-operators/
