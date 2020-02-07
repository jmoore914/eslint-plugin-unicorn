# Prefer ternary expressions over simple `if/then/else` statements

This rule enforces the use of ternary expressions over  'simple' `if/then/else` statements where 'simple' means the consequent and alternate are each one line and have the same basic type and form.

Using an `if/then/else` statement typically results in more lines of code than a single lined ternary expression, which leads to an unnecessarily larger codebase that is more difficult to maintain.

Additionally, using an `if/then/else` statement can result in defining variables using `let` or `var` solely to be reassigned within the blocks. This leads to varaibles being unnecessarily mutable and prevents `prefer-const` from flagging the variable.

This rule is fixable.


## Fail

```js
let foo =''
if(bar){
	foo = 3
}
else{
	foo = 4
}
```

```js
if(bar){
	return 3
}
else{
	return 4
}
```

## Pass

```js
let foo = bar ? 3 : 4
```

```js
return bar ? 3 : 4
```


```js
let foo = ''
if(bar){
	baz()
	foo = 3
}
else{
	foo = 4
}
```

```js
if(bar){
	foo = 3
}
else{
	return 4
}
```

## Options

This rule can take the following options:
* An object with the following keys: 'assignment', 'return', 'call'
* The string 'always'

### assignment
The assignment option determines whether the rule will flag assignment expressions. It can take the following values: 'never', 'same', 'always'. Default value is 'same'.

**never**: the rule will not flag any assignment statements. 
With `{assigment: 'never'}` the following would both NOT be flagged:
```js
let foo =''
if(bar){
	foo = 3
}
else{
	foo = 4
}
```

```js
let foo =''
if(bar){
	foo = 3
}
else{
	baz = 4
}
```

**same**: the rule will flag assignment statements assigning to the same variable. 
With `{assigment: 'same'}` the following would be flagged:
```js
let foo =''
if(bar){
	foo = 3
}
else{
	foo = 4
}
```
With `{assigment: 'same'}` the following would NOT be flagged:
```js
let foo =''
if(bar){
	foo = 3
}
else{
	baz = 4
}
```


**always**: the rule will flag all assignment statements. 
With `{assigment: 'always'}` the following would both be flagged:
```js
let foo =''
if(bar){
	foo = 3
}
else{
	foo = 4
}
```

```js
let foo =''
if(bar){
	foo = 3
}
else{
	baz = 4
}
```

### return
The return option determines whether the rule will flag return expressions. It can take a boolean. Default value is true.
With `{return: false}` the following would NOT be flagged:
```js
let foo =''
if(bar){
	return 3
}
else{
	return 4
}
```

### call
The call option determines whether the rule will flag call expressions. It can take a boolean. Default value is false.
With `{call: true}` the following would be flagged:
```js
if(bar){
	foo()
}
else{
	baz()
}
```


### 'always'

Always prefer ternary to simple `if/then/else` statements. This option is equivalent to ```{assignment: 'always', return: true, call:true}```.