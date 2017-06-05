**HOTKEY:**

case:camel-underscore (ALT-SHIFT-COMMAND + X): fooBar(or FooBar) <-> foo_bar

case:upper-lower (ALT-SHIFT-COMMAND + S): FOOBAR <-> foobar

**script(camel-underscore):**

if {query} contains "_" char, to CamelCase, else to underscore.
The first letter of the output is always lowercase.

```
if [[ "{query}" =~ "_" ]]; then
    echo -n "{query}" | perl -pe 's/^([A-Z]+)/\L$1/g' |perl -pe 's/(_)./uc($&)/ge;s/_//g'
else
    echo -n "{query}" | perl -pe 's/^([A-Z]+)/\L$1/g' | perl -pe 's/([a-z0-9])([A-Z]+)/$1_\L$2/g'
fi
``` 

**script(upper-lower):**

if {query} contains any "A-Z" char, to lowercase, else to uppercase

```
if [[ "{query}" =~ [A-Z] ]]; then
    echo -n "{query}" | tr '[A-Z]' '[a-z]'
else
    echo -n "{query}" | tr '[a-z]' '[A-Z]'
fi
```

