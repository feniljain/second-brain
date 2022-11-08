## Frequently used constructs

- Check if a variable is empty:
```bash
if [ -z "$var" ]
then
      echo "\$var is empty"
else
      echo "\$var is NOT empty"
fi
```

- Setting default value for a parameter
```bash
# varName=${<variable-number>:-default value}
# e.g.
parentBranch=${1:-staging}
```