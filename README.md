# greps_test

The following oneliner extracts varibles from bash code:
```bash
grep -Po '\\*?\$.*?[" }\n]' | grep -v '^\\[^\]' | sed -e 's|\\||'
```
Usage:
```bash
cat vars.test | grep -Po '\\*?\$.*?[" }\n]' | grep -v '^\\[^\]' | sed -e 's|\\||'  
```
Expected output:
```bash
$plain_var 
$concatenated$vars 
${expanded_var}
${multiline_var4}
$multiline_var5 
${arr1e}
\${arr2e}
${CHANNEL:-common}
${1}
\${two_slashes_to_one}
```
Explanation:

1. 
```bash
grep -Po '\\*?\$.*?[" }\n]' 
```
searches for words starting with 0 or more leading backslashes followed by the dollar sign, with any characters afer it ending with space, closing curly brace or the newline symbol.

2. 
```bash
grep -v '^\\[^\]'
```
rejects all the vars starting with one backslash

3. 
```bash
sed -e 's|\\||'
 ``` 
replaces two b/slashes with one.
