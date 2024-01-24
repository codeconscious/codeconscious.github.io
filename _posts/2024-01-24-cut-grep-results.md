# Using `cut` with `grep` results

I learned how to extract just the file names and line numbers from `grep` output (excluding the matched content itself):

```shell
grep -Rn . --include \*.rb --include \*.erb -e 'pluralize` | cut -f1,2 -d:
```

Here, `cut` truncates the output of each `grep`ped line after and including the second colon, leaving just the file path and line number.
