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

- `set -e` stops the script on errors 
- `set -u` stops the script on unset variables
- `set -o pipeline` 
	- curl 404.com | grep 'panda'
		- curl failed but grep succeeds
	- above command prevents this