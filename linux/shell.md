## Executing for each line

```sh
lines | while read line; do echo $line; done
while read line; do echo $line; done < file
```

## Coreutils

| command | description                    |
| ------- | ------------------------------ |
| tac     | for reversing the output       |
| nl      | adds line numbers to each line |
