In vim, delete all text that is not matched by the pattern `text`

```
:%s/\(^\|\(text\)\@<=\).\{-}\($\|text\)\@=//g
```





