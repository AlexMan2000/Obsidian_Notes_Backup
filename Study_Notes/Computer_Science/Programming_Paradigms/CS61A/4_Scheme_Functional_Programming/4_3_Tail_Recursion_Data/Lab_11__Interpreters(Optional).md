> The questions in this assignment are not graded, but they are highly recommended to help you prepare for the Scheme project.
> - If you are in a regular section, you will automatically get the 1 completion point. However, attendance is still required to get the attendance point.
> - If you are in the mega section, you will automatically get both points for this lab.

[released_lab_lab11_lab11.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1672999903919-d6bd58bd-499d-4dd0-a798-92550cd4a8a0.zip)
[released_lab_sol-lab11_lab11.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1672999903929-e5c97730-233b-402f-9874-7073a06f0e3a.zip)
[Lab 11_ Interpreters _ CS 61A Fall 2022.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1672999939173-be0c44e2-ad89-4580-bce0-aa439f4edaa0.pdf)

# Introduction
> ![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022454062.png)



# Part 1 
## Context
> ![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022466902.png)



## P1: Buffer⭐⭐⭐
> ![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022465469.png)
> 此题比较易错

```python
class Buffer:
    """A Buffer provides a way of accessing a sequence of tokens across lines.

    Its constructor takes an iterator, called "the source", that returns the
    next line of tokens as a list each time it is queried, or None to indicate
    the end of data.

    The Buffer in effect concatenates the sequences returned from its source
    and then supplies the items from them one at a time through its pop_first()
    method, calling the source for more sequences of items only when needed.

    In addition, Buffer provides a current method to look at the
    next item to be supplied, without sequencing past it.

    The __str__ method prints all tokens read so far, up to the end of the
    current line, and marks the current token with >>.
    >>> buf = Buffer(iter([['(', '+'], [15], [12, ')']]))
    >>> buf.pop_first()
    '('
    >>> buf.pop_first()
    '+'
    >>> buf.current()
    15
    >>> buf.current()   # Calling current twice should not change buf
    15
    >>> buf.pop_first()
    15
    >>> buf.current()
    12
    >>> buf.pop_first()
    12
    >>> buf.pop_first()
    ')'
    >>> buf.pop_first()  # returns None
    """

    def __init__(self, source):
        """
        Initialize a Buffer instance based on the given source.
        """
        self.index = 0
        self.source = source
        self.current_line = ()
            self.current()

            def pop_first(self):
                """Remove the next item from self and return it. If self has
        exhausted its source, returns None."""
        # BEGIN PROBLEM 1
        "*** YOUR CODE HERE ***"
        # END PROBLEM 1

    def current(self):
        """Return the current element, or None if none exists."""
        while _________:
            try:
                # BEGIN PROBLEM 1
                "*** YOUR CODE HERE ***"
                # END PROBLEM 1
            except StopIteration:
                self.current_line = ()
                    return None
        return __________

    def more_on_line(self):
    	return self.index < len(self.current_line)
```
```python
class Buffer:
    """A Buffer provides a way of accessing a sequence of tokens across lines.

    Its constructor takes an iterator, called "the source", that returns the
    next line of tokens as a list each time it is queried, or None to indicate
    the end of data.

    The Buffer in effect concatenates the sequences returned from its source
    and then supplies the items from them one at a time through its pop_first()
    method, calling the source for more sequences of items only when needed.

    In addition, Buffer provides a current method to look at the
    next item to be supplied, without sequencing past it.

    The __str__ method prints all tokens read so far, up to the end of the
    current line, and marks the current token with >>.
    >>> buf = Buffer(iter([['(', '+'], [15], [12, ')']]))
    >>> buf.pop_first()
    '('
    >>> buf.pop_first()
    '+'
    >>> buf.current()
    15
    >>> buf.current()   # Calling current twice should not change buf
    15
    >>> buf.pop_first()
    15
    >>> buf.current()
    12
    >>> buf.pop_first()
    12
    >>> buf.pop_first()
    ')'
    >>> buf.pop_first()  # returns None
    """

    def __init__(self, source):
        """
        Initialize a Buffer instance based on the given source.
        """
        self.index = 0
        self.source = source
        self.current_line = ()
        self.current()

    # Then implement this
    def pop_first(self):
        """Remove the next item from self and return it. If self has
        exhausted its source, returns None."""
        # BEGIN PROBLEM 1
        # 调用current是为了利用function abstraction, 借用current中的
        # 边界条件判断，否则会造成数组越界
        # 比如res = self.current_line[self.index]
        res = self.current()
        self.index += 1
        return res
        # END PROBLEM 1

    # First implement this
    def current(self):
        """Return the current element, or None if none exists."""
        # 直到下一个有tokens的列表为止
        while not self.more_on_line():
            try:
                # BEGIN PROBLEM 1
                "*** YOUR CODE HERE ***"
                self.index = 0
                self.current_line = next(self.source)
                # END PROBLEM 1
            except StopIteration:
                self.current_line = ()
                return None

        # 返回列表的第一个元素
        return self.current_line[self.index]

    def more_on_line(self):
        return self.index < len(self.current_line)
```


# Part 2
## Internal Representation
> ![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022466969.png)
> 总之, `scheme_reader`返回的结构一定是`Pair(..., Pair(...))`, 其中`...`可以是`internal representation`或者是`Pair`对象。



## P2: Mutual Recursion⭐⭐⭐⭐⭐
> ![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022462587.png)![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022467011.png)

```python
# Scheme list parser


def scheme_read(src):
    """Read the next expression from SRC, a Buffer of tokens.

    >>> scheme_read(Buffer(tokenize_lines(['nil'])))
    nil
    >>> scheme_read(Buffer(tokenize_lines(['1'])))
    1
    >>> scheme_read(Buffer(tokenize_lines(['true'])))
    True
    >>> scheme_read(Buffer(tokenize_lines(['(+ 1 2)'])))
    Pair('+', Pair(1, Pair(2, nil)))
    """
    if src.current() is None:
        raise EOFError
    val = src.pop_first()  # Get and remove the first token
    if val == 'nil':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        # END PROBLEM 2
    elif val == '(':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        # END PROBLEM 2
    elif val == "'":
        # BEGIN PROBLEM 3
        "*** YOUR CODE HERE ***"
        # END PROBLEM 3
    elif val not in DELIMITERS:
        return val
    else:
        raise SyntaxError('unexpected token: {0}'.format(val))


def read_tail(src):
    """Return the remainder of a list in SRC, starting before an element or ).

    >>> read_tail(Buffer(tokenize_lines([')'])))
    nil
    >>> read_tail(Buffer(tokenize_lines(['2 3)'])))
    Pair(2, Pair(3, nil))
    """
    try:
        if src.current() is None:
            raise SyntaxError('unexpected end of file')
        elif src.current() == ')':
            # BEGIN PROBLEM 2
            "*** YOUR CODE HERE ***"
            # END PROBLEM 2
        else:
            # BEGIN PROBLEM 2
            "*** YOUR CODE HERE ***"
            # END PROBLEM 2
    except EOFError:
        raise SyntaxError('unexpected end of file')
```
```python

# Scheme list parser


def scheme_read(src):
    """Read the next expression from SRC, a Buffer of tokens.

    >>> scheme_read(Buffer(tokenize_lines(['nil'])))
    nil
    >>> scheme_read(Buffer(tokenize_lines(['1'])))
    1
    >>> scheme_read(Buffer(tokenize_lines(['true'])))
    True
    >>> scheme_read(Buffer(tokenize_lines(['(+ 1 2)'])))
    Pair('+', Pair(1, Pair(2, nil)))
    """
    if src.current() is None:
        raise EOFError
    val = src.pop_first()  # Get and remove the first token
    if val == 'nil':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        return nil   # 注意是nil object, 而不是nil字符串
        # END PROBLEM 2
    elif val == '(':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        return read_tail(src)  # 上面的代码已经pop_first了，所以这里不需要再pop_first()
        # END PROBLEM 2
    elif val == "'":
        # BEGIN PROBLEM 3
        "*** YOUR CODE HERE ***"
        # END PROBLEM 3
    elif val not in DELIMITERS:
        return val
    else:
        raise SyntaxError('unexpected token: {0}'.format(val))


def read_tail(src):
    """Return the remainder of a list in SRC, starting before an element or ).

    >>> read_tail(Buffer(tokenize_lines([')'])))
    nil
    >>> read_tail(Buffer(tokenize_lines(['2 3)'])))
    Pair(2, Pair(3, nil))
    """
    try:
        if src.current() is None:
            raise SyntaxError('unexpected end of file')
        elif src.current() == ')':
            # BEGIN PROBLEM 2
            "*** YOUR CODE HERE ***"
            src.pop_first()
            return nil
            # 注意这个return nil就是我们的递归终止处。
            # END PROBLEM 2
        else:
            # BEGIN PROBLEM 2
            "*** YOUR CODE HERE ***"
            complete_expression = scheme_read(src)  # 读取完当前的expression
            rest_of_combination = read_tail(src)  
            # 如果又遇到了(,就开启新一轮scheme_read, 否则在80行处返回, 跳转到scheme_read中
            # complete_expression 是primitive expression 或者Pair
            # rest_of_combination 是Pair数据结构
            return Pair(complete_expression, rest_of_combination)
            # END PROBLEM 2
    except EOFError:
        raise SyntaxError('unexpected end of file')

```


## P3: Scheme Reader⭐⭐
> ![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022462328.png)

**Test Examples**![image.png](./Lab_11__Interpreters(Optional).assets/20230302_1022463568.png)
```python
def scheme_read(src):
    """Read the next expression from SRC, a Buffer of tokens.

    >>> scheme_read(Buffer(tokenize_lines(['nil'])))
    nil
    >>> scheme_read(Buffer(tokenize_lines(['1'])))
    1
    >>> scheme_read(Buffer(tokenize_lines(['true'])))
    True
    >>> scheme_read(Buffer(tokenize_lines(['(+ 1 2)'])))
    Pair('+', Pair(1, Pair(2, nil)))
    """
    if src.current() is None:
        raise EOFError
    val = src.pop_first()  # Get and remove the first token
    if val == 'nil':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        return nil   # 注意是nil object, 而不是nil字符串
        # END PROBLEM 2
    elif val == '(':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        return read_tail(src)  # 上面的代码已经pop_first了，所以这里不需要再pop_first()
        # END PROBLEM 2
    elif val == "'":
        # BEGIN PROBLEM 3
        "*** YOUR CODE HERE ***"
        # END PROBLEM 3
    elif val not in DELIMITERS:
        return val
    else:
        raise SyntaxError('unexpected token: {0}'.format(val))
```
```python
def scheme_read(src):
    """Read the next expression from SRC, a Buffer of tokens.

    >>> scheme_read(Buffer(tokenize_lines(['nil'])))
    nil
    >>> scheme_read(Buffer(tokenize_lines(['1'])))
    1
    >>> scheme_read(Buffer(tokenize_lines(['true'])))
    True
    >>> scheme_read(Buffer(tokenize_lines(['(+ 1 2)'])))
    Pair('+', Pair(1, Pair(2, nil)))
    """
    if src.current() is None:
        raise EOFError
    val = src.pop_first()  # Get and remove the first token
    if val == 'nil':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        return nil   # 注意是nil object, 而不是nil字符串
        # END PROBLEM 2
    elif val == '(':
        # BEGIN PROBLEM 2
        "*** YOUR CODE HERE ***"
        return read_tail(src)  # 上面的代码已经pop_first了，所以这里不需要再pop_first()
        # END PROBLEM 2
    elif val == "'":
        # BEGIN PROBLEM 3
        "*** YOUR CODE HERE ***"
        return Pair('quote', Pair(scheme_read(src),nil))
        # END PROBLEM 3
    elif val not in DELIMITERS:
        return val
    else:
        raise SyntaxError('unexpected token: {0}'.format(val))
```
