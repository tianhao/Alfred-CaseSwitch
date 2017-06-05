## Usage

### FOOBAR ⇌ foobar

Alfred keyword: case-upper-lower

shortcut key: ⌥ ⇧ ⌘ + U

### fooBar ⇌ foo_bar

Alfred keyword: case-camel-underscore

shortcut key: ⌥ ⇧ ⌘ + X

### foo-bar ⇌ fooBar

Alfred keyword: case-snake-camel

shortcut key: ⌥ ⇧ ⌘ + S

**You can modify the keyword or shortcut key**

## scripts

**script(upper-lower):**

if {query} contains any "A-Z" char, to lowercase, else to uppercase

```
if [[ "{query}" =~ [A-Z] ]]; then
    echo -n "{query}" | tr '[A-Z]' '[a-z]'
else
    echo -n "{query}" | tr '[a-z]' '[A-Z]'
fi
```


**script(camel-underscore):**

if {query} contains "_" char, to camelCase, else to underscore.

The first letter of the output is always lowercase.

```
if [[ "{query}" =~ "_" ]]; then
    echo -n "{query}" | perl -pe 's/^([A-Z]+)/\L$1/g' |perl -pe 's/(_)./uc($&)/ge;s/_//g'
else
    echo -n "{query}" | perl -pe 's/^([A-Z]+)/\L$1/g' | perl -pe 's/([a-z0-9])([A-Z]+)/$1_\L$2/g'
fi
``` 

**script(snake-camel):**

if {query} contains "-" char, to camelCase, else to snakeCase

The first letter of the output is always lowercase.

```
if [[ "{query}" =~ "-" ]]; then
    echo -n "{query}" | perl -pe 's/^([A-Z]+)/\L$1/g' |perl -pe 's/(-)./uc($&)/ge;s/-//g'
else
    echo -n "{query}" | perl -pe 's/^([A-Z]+)/\L$1/g' | perl -pe 's/([a-z0-9])([A-Z]+)/$1-\L$2/g'
fi
```


