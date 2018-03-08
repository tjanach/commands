# Python 2 scripting

+ check python version
```sh
$ python -V
```
+ enter python interactive shell
```sh
$ python
```
+ close python interactive shell
```sh
ctrl+d
```
+ simple input script
```python
#!/usr/bin/python

print ("Please enter your name: ")
input = raw_input()
print ("Hello "+input)
```
+ if statement 
    + indentation 4 spaces !!!
    + colon (:) before code
```python
#!/usr/bin/python
if condition:
    code
elif condition:
    code
else:
    code
```
___
```python
#!/usr/bin/python
import sys
if (len(sys.argv)==1):
    print ("Usage "+sys.argv[0]+" username")
```
+ arrays, tuples, dictionaries
```python
#!/usr/bin/python
my_arr = [val1, val2, val3]
my_arr[index]
my_tuple = (val1, val2, val3)
my_tuple[index]
my_dict = {key1:val1, key2:val2, key3:val3}
my_dict[key]
```
___
+ loops
```python
#!/usr/bin/python
for item in item_sequence:
    code
while (condition):
    code
    
while (True):
    code
    time.sleep(1s)
```
```python
#!/usr/bin/python
import sys
i = 1
for arg in sys.argv:
    print ("Arg "+str(i)+" is "+ arg)
    i = i + 1
```
