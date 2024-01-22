[released_hw_hw06_hw06.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1672753989593-ecb48b6c-00c7-498a-ac7b-fc6e0645aeea.zip)
[released_hw_sol-hw06_hw06.zip](https://www.yuque.com/attachments/yuque/0/2023/zip/12393765/1672753989669-f7f013ea-c8df-44da-8891-b31f82d4a4d1.zip)
[Homework 6 _ CS 61A Fall 2022.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1672754029767-5770bfde-2450-47ac-9545-1b19d0386d39.pdf)
[Homework 6 Solutions _ CS 61A Fall 2022.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1672754031148-6ef6d043-feff-4906-bae2-8de73dfd3c58.pdf)


# OOP
## Q1: Mint - Class Attributes⭐⭐⭐⭐⭐
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018019076.png)
> 注意这个`plus one extra for each year of age beyond 50`, 如果不是`beyond 50`就不用加。

```python
class Mint:
    """A mint creates coins by stamping on years.

    The update method sets the mint's stamp to Mint.present_year.

    >>> mint = Mint()
    >>> mint.year
    2022
    >>> dime = mint.create(Dime)
    >>> dime.year
    2022
    >>> Mint.present_year = 2102  # Time passes
    >>> nickel = mint.create(Nickel)
    >>> nickel.year     # The mint has not updated its stamp yet
    2022
    >>> nickel.worth()  # 5 cents + (80 - 50 years)
    35
    >>> mint.update()   # The mint's year is updated to 2102
    >>> Mint.present_year = 2177     # More time passes
    >>> mint.create(Dime).worth()    # 10 cents + (75 - 50 years)
    35
    >>> Mint().create(Dime).worth()  # A new mint has the current year
    10
    >>> dime.worth()     # 10 cents + (155 - 50 years)
    115
    >>> Dime.cents = 20  # Upgrade all dimes!
    >>> dime.worth()     # 20 cents + (155 - 50 years)
    125
    """
    present_year = 2022

    def __init__(self):
        self.update()

    def create(self, coin):
        "*** YOUR CODE HERE ***"

    def update(self):
        "*** YOUR CODE HERE ***"

```
```python
class Mint:
    """A mint creates coins by stamping on years.

    The update method sets the mint's stamp to Mint.present_year.

    >>> mint = Mint()
    >>> mint.year
    2022
    >>> dime = mint.create(Dime)
    >>> dime.year
    2022
    >>> Mint.present_year = 2102  # Time passes
    >>> nickel = mint.create(Nickel)
    >>> nickel.year     # The mint has not updated its stamp yet
    2022
    >>> nickel.worth()  # 5 cents + (80 - 50 years)
    35
    >>> mint.update()   # The mint's year is updated to 2102
    >>> Mint.present_year = 2177     # More time passes
    >>> mint.create(Dime).worth()    # 10 cents + (75 - 50 years)
    35
    >>> Mint().create(Dime).worth()  # A new mint has the current year
    10
    >>> dime.worth()     # 10 cents + (155 - 50 years)
    115
    >>> Dime.cents = 20  # Upgrade all dimes!
    >>> dime.worth()     # 20 cents + (155 - 50 years)
    125
    """
    present_year = 2022

    def __init__(self):
        self.update()

    def create(self, coin):
        "*** YOUR CODE HERE ***"
        return coin(self.year)


    def update(self):
        "*** YOUR CODE HERE ***"
        self.year = self.present_year  # Mint.present_year 也可以




class Coin:
    cents = None  # will be provided by subclasses, but not by Coin itself

    def __init__(self, year):
        self.year = year

    def worth(self):
        "*** YOUR CODE HERE ***"
        return self.cents + max(0, Mint.present_year - self.year - 50)


class Nickel(Coin):
    cents = 5


class Dime(Coin):
    cents = 10
```

# Linked List
## Q2 Store Digits⭐⭐⭐
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018012404.png)

```python
def store_digits(n):
    res = Link.empty
    while n > 10:
        n, res = n // 10, Link(n % 10, res)

    return Link(n, res)

# Alt
def store_digits(n):
    result = Link.empty
    while n > 0:
        result = Link(n % 10, result)
        n //= 10
    return result

```


## Q3 Mutable Mapping
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018021259.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018022835.png)

```python
def deep_map_mut(func, lnk):
    """Mutates a deep link lnk by replacing each item found with the
    result of calling func on the item.  Does NOT create new Links (so
    no use of Link's constructor).

    Does not return the modified Link object.

    >>> link1 = Link(3, Link(Link(4), Link(5, Link(6))))
    >>> # Disallow the use of making new Links before calling deep_map_mut
    >>> Link.__init__, hold = lambda *args: print("Do not create any new Links."), Link.__init__
    >>> try:
    ...     deep_map_mut(lambda x: x * x, link1)
    ... finally:
    ...     Link.__init__ = hold
    >>> print(link1)
    <9 <16> 25 36>
    """
    "*** YOUR CODE HERE ***"
    if lnk == Link.empty:
        return

    if isinstance(lnk.first, Link):
        deep_map_mut(func, lnk.first)
    else:
        lnk.first = func(lnk.first)
    deep_map_mut(func, lnk.rest)

```
```python
def deep_map_mut(func, lnk):
    """Mutates a deep link lnk by replacing each item found with the
    result of calling func on the item.  Does NOT create new Links (so
    no use of Link's constructor).

    Does not return the modified Link object.

    >>> link1 = Link(3, Link(Link(4), Link(5, Link(6))))
    >>> # Disallow the use of making new Links before calling deep_map_mut
    >>> Link.__init__, hold = lambda *args: print("Do not create any new Links."), Link.__init__
    >>> try:
    ...     deep_map_mut(lambda x: x * x, link1)
    ... finally:
    ...     Link.__init__ = hold
    >>> print(link1)
    <9 <16> 25 36>
    """
    if lnk is Link.empty:
        return
    elif isinstance(lnk.first, Link):
        deep_map_mut(func, lnk.first)
    else:
        lnk.first = func(lnk.first)
    deep_map_mut(func, lnk.rest)

```

## Q4 Two List⭐⭐⭐
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018029489.png)
> **本题提供两种思路:**
> 一种是采用迭代的方法:
> 1. 正向迭代，运用指针和面向对象的思维(通过访问对象属性`l.rest, l.first`完成链表构建), 也就是我们先创建一个`linked list`, 然后定义一个指针`p`指向当前元素，然后逐个往后迭代创建完整的链表。
> 2. 反向迭代, 注意由于我们的链表结构是`Link(3, Link(...))`，我们在`Link`的时候必须从尾部开始链接，所以需要反向遍历列表。
> 
第二种递归的方法会有些困难: 这是一种深度优先的递归方法，即我们必须先下探到列表`vals`中的最后一个元素，从这个元素开始构建列表。

```python
def two_list(vals, counts):
    """
    Returns a linked list according to the two lists that were passed in. Assume
    vals and counts are the same size. Elements in vals represent the value, and the
    corresponding element in counts represents the number of this value desired in the
    final linked list. Assume all elements in counts are greater than 0. Assume both
    lists have at least one element.

    >>> a = [1, 3, 2]
    >>> b = [1, 1, 1]
    >>> c = two_list(a, b)
    >>> c
    Link(1, Link(3, Link(2)))
    >>> a = [1, 3, 2]
    >>> b = [2, 2, 1]
    >>> c = two_list(a, b)
    >>> c
    Link(1, Link(1, Link(3, Link(3, Link(2)))))
    """
    "*** YOUR CODE HERE ***"
    assert len(vals) == len(counts), "the lists' size don't match"
    res = Link(None)
    # Pointer start at the beginning
    p = res
    for index in range(len(counts)):
        elem, times = vals[index], counts[index]
        for _ in range(times):
            p.rest = Link(elem)
            # 往后迭代
            p = p.rest

    return res.rest
```
```python
def two_list(vals, counts):
    """
    Returns a linked list according to the two lists that were passed in. Assume
    vals and counts are the same size. Elements in vals represent the value, and the
    corresponding element in counts represents the number of this value desired in the
    final linked list. Assume all elements in counts are greater than 0. Assume both
    lists have at least one element.

    >>> a = [1, 3, 2]
    >>> b = [1, 1, 1]
    >>> c = two_list(a, b)
    >>> c
    Link(1, Link(3, Link(2)))
    >>> a = [1, 3, 2]
    >>> b = [2, 2, 1]
    >>> c = two_list(a, b)
    >>> c
    Link(1, Link(1, Link(3, Link(3, Link(2)))))
    """
    "*** YOUR CODE HERE ***"
    res = Link.empty
    for elem, times in zip(reversed(vals), reversed(counts)):
        for i in range(times):
            res = Link(elem, res)

    return res
```
```python
def two_list(vals, counts):
    if len(vals) == 1:
        res = Link.empty
        for i in range(counts[0]):
            res = Link(vals[0], res)
        return res

    # 先下探，不构建
    res = two_list(vals[1:], counts[1:])
    # 之后的链表都构建完了才构建当前元素
    for i in range(counts[0]):
        res = Link(vals[0], res)
    return res

```


# Optional Questions
## *Q5 Next Virahanka Fib Object
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018021872.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018024955.png)



## Q6 Is BST⭐⭐⭐⭐⭐
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018034557.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018032525.png)
> 本题我们提供两种方法，都非常经典：
> 1. 定义一个函数`is_BST_helper(t, bmin, bmax)`，这种方法从子树的角度考虑，是一种`preorder`, 也就是我们通过`is_BST_helper`给子树里面所有的节点规定了上下界`[bmin,bmax]`，在后续的遍历中，一旦子树中有一个节点突破了这个界限，就报错，不是一棵合法的`BST`。
> 2. 定义两个函数`bmin(t)`, `bmax(t)`, `bmin(t)`返回以当前`node`为根节点的二叉树中的最小值, `bmax(t)`返回以当前`node`为根节点的二叉树中的最大值, 这种方法非常容易理解，但是代码不够精简。这种方法从节点的角度考虑，先在左子树中计算出最大值`leftmax`，然后在右子树中计算出最小值`rightmin`，然后看看当前节点是否落在`[leftmax, rightmin-1]`之间。

```python
def is_bst(t):
    def helper(t, minv, maxv):
        # 剪枝
        if t.label < minv or t.label > maxv or len(t.branches) > 2:
            return False
    	# 到了叶子节点必须判断是否在[minv, maxv]之间
        if t.is_leaf():
            return minv <= t.label <= maxv

        elif len(t.branches) == 1:
            b = t.branches[0]
            # 规定子树的取值范围
            return helper(b, minv, t.label) or helper(b, t.label + 1, maxv)
        elif len(t.branches) == 2:
            left, right = t.branches[0], t.branches[1]
            return helper(left, minv, t.label) and helper(right, t.label + 1, maxv)
            
    return helper(t, float("-inf"), float("inf"))
```
```python
def is_bst(t):
    def bmin(t):
        if t.is_leaf():
            return t.label
        return min([t.label]+ [bmin(b) for b in t.branches])

    def bmax(t):
        if t.is_leaf():
            return t.label
        return max([t.label] + [bmax(b) for b in t.branches])

    # 叶子节点当然是BST
    if t.is_leaf():
        return True
    # 如果只有左子树
    elif len(t.branches) == 1:
        b = t.branches[0]
        return is_bst(b) and (t.label < bmin(b) or t.label >= bmax(b))
    # 如果左右子树都有, 需要判断大小关系
    elif len(t.branches) == 2:
        left, right = t.branches[0],t.branches[1]
        return bmax(left) <= t.label < bmin(right) and is_bst(left) and is_bst(right)
    # 如果有多于两个branches, 就说明这都不是一颗二叉树，更别说是二叉搜索树了
    else:
        return False
```



# Exam Practice
## OOP
### *Q7 OOP Version of Hog Project
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018034202.png)

**Problem (a)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018038539.png)
**Problem (b)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018033527.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018032504.png)
**Problem (c)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018041034.png)
**Problem (d)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018041178.png)
**Problem (e)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018046813.png)
**Problem (f)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018048258.png)
```python
# Q7
class HoopDice:
    def __init__(self, values):
        """Initialize a dice with possible values VALUES, and a starting INDEX
        of 0. The INDEX indicates which value from VALUES to return when the
        dice is rolled next.
        """
        self.values = values
        self.index = 0
    def roll(self):
        """Roll this dice. Advance the index to the next step before returning.
        """
        value = ______________
        ______________ = (______________) % ______________
        return value

    def next_player(self):
        """Infinitely yields the next player in the game, in order.
        >>> player_gen = game.next_player()
        >>> next(player_gen) is player1
        True
        >>> next(player_gen) is player3
        False
        >>> next(player_gen) is player3
        True
        >>> next(player_gen) is player1
        True
        >>> next(player_gen) is player2
        True
        >>> new_player_gen = game.next_player()
        >>> next(new_player_gen) is player1
        True
        >>> next(player_gen) is player3
        True
        """

        yield from ______________
        yield from ______________

    def get_scores_except(self, player):
        """Collects and returns a list of the current scores for all players
        except PLAYER.
        >>> game.get_scores_except(player2)
        [0, 0]
        """

        return [______________ for pl in ______________ if ______________]

    def roll_dice(self, num_rolls):
        """Simulate rolling SELF.DICE exactly NUM_ROLLS > 0 times. Return sum of
        the outcomes unless any of the outcomes is 1. In that case, return 1.
        >>> game.roll_dice(4)
        20
        """

        outcomes = [______________ for x in ______________]
        ones = [______________ for outcome in outcomes]
        return 1 if ______________(ones) else ______________(outcomes)

    def play(self):
        """Play the game while no player has reached or exceeded the goal score.
        After the game ends, return all players' scores.
        >>> game.play()
        [20, 10, 60]
        """
        player_gen = self.next_player()
        while max(self.get_scores()) < self.goal:
            player = ______________(player_gen)
            other_scores = self.get_scores_except(player)
            num_rolls = ______________(player.score, other_scores)
            outcome = self.roll_dice(num_rolls)
            ______________ += outcome
            return self.get_scores()


class BrokenHoopDice(HoopDice):
    def __init__(self, values, when_broken):
        ______________(values)
        self.when_broken = when_broken
        self.______________ = False

    def roll(self):
        """
        >>> broken = BrokenHoopDice([5, 6, 7], 11)
        >>> broken.roll()
        5
        >>> [broken.roll() for _ in range(6)]
        [11, 6, 11, 7, 11, 5]
        """
        if self.is_broken:
            self.is_broken = not self.is_broken
            return ______________
        else:
            self.is_broken = not self.is_broken
            return ______________()



```


### *Q8 Sparse Lists
**Problem Description**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018047085.png)
**Problem (a)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018043043.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018056166.png)
**Problem (b)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018052509.png)
**Problem (c)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018058736.png)
```python
class SparseList:
    """Represent a non-empty list as a most common value and a dictionary from
    indices to values that contains only values that are not the most common.
    >>> pi = SparseList([3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5])
    >>> pi.common
    5
    >>> pi.others
    {0: 3, 1: 1, 2: 4, 3: 1, 5: 9, 6: 2, 7: 6, 9: 3}
    >>> [pi.item(0), pi.item(1), pi.item(2), pi.item(3), pi.item(4)]
    [3, 1, 4, 1, 5]
    >>> pi.item(10)
    5
    >>> pi.item(11)
    'out of range'
    >>> pi.items()
    [3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5]
    """
    def __init__(self, s):
        pass
    def item(self, i):
        pass
    def items(self):
        pass
```


### Q9 Version 2.0⭐⭐⭐
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018058705.png)
> 本题比较有意思，利用了`special methods``__str__`的递归调用模式。
> 同时要注意，`python`的字符串是可以通过`+`直接拼接的。

```python
class Version:
    """A version of a string after an edit.
    >>> s = Version('No power?', Delete(3, 6))
    >>> print(Version(s, Insert(3, 'class!')))
    No class!
    >>> t = Version('Beary', Insert(4, 'kele'))
    >>> print(t)
    Bearkeley
    >>> print(Version(t, Delete(2, 1)))
    Berkeley
    >>> print(Version(t, Delete(4, 5)))
    Bear
    """
    def __init__(self, previous, edit):
        self.previous, self.edit = previous, edit
    def __str__(self):
        return ____________________________________


class Edit:
    def __init__(self, i, c):
        self.i, self.c = i, c

class Insert(Edit):
    def apply(self, t):
        "Return a new string by inserting string c into t starting at position i."
        return _____________________________________


class Delete(Edit):
    def apply(self, t):
        "Return a new string by deleting c characters from t starting at position i."
        return _____________________________________
```
```python
class Version:
    """A version of a string after an edit.
    >>> s = Version('No power?', Delete(3, 6))
    >>> print(Version(s, Insert(3, 'class!')))
    No class!
    >>> t = Version('Beary', Insert(4, 'kele'))
    >>> print(t)
    Bearkeley
    >>> print(Version(t, Delete(2, 1)))
    Berkeley
    >>> print(Version(t, Delete(4, 5)))
    Bear
    """
    def __init__(self, previous, edit):
        self.previous, self.edit = previous, edit


    def __str__(self):
        return f'{self.edit.apply(str(self.previous))}'


class Edit:
    def __init__(self, i, c):
        self.i, self.c = i, c

class Insert(Edit):
    def apply(self, t):
        "Return a new string by inserting string c into t starting at position i."
        return ''.join(list(t)[:self.i]+list(self.c)+list(t)[self.i:])
    	# return t[:self.i] + self.c + t[self.i:]

class Delete(Edit):
    def apply(self, t):
        "Return a new string by deleting c characters from t starting at position i."
        return ''.join(list(t)[:self.i]+list(t)[self.i+self.c:])
        # return t[:self.i] + t[self.i + self.c:]

```


## Linked Lists
### *Q10 College Party
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018051651.png)

**Problem (a)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018057343.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018054535.png)
**Problem (b)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018059449.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018067506.png)
**Problem (c)**![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018069955.png)![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018067587.png)
```python
def wins(states, k):
    """Yield each linked list of two-letter state codes that describes a win by at least k.
    >>> print_all(wins(battleground, 50))
    <AZ PA NV GA WI MI>
    <AZ PA NV GA MI>
    <AZ PA GA WI MI>
    <PA NV GA WI MI>
    >>> print_all(wins(battleground, 75))
    <AZ PA NV GA WI MI>
    """
    if _________:
        yield Link.empty
    if states:
        first = states[0].electors
        for win in wins(states[1:], _________):
            yield Link(_________, win)
        yield from wins(states[1:], _________)



def must_win(states, k):
    """List all states that must be won in every scenario that wins by k.
    >>> must_win(battleground, 50)
    ['PA', 'GA', 'MI']
    >>> must_win(battleground, 75)
    ['AZ', 'PA', 'NV', 'GA', 'WI', 'MI']
    """
    def contains(s, x):
        """Return whether x is a value in linked list s."""
        return (_________) and (_________)
    # (a) (b)
    return [_________ for s in states if _________([_________ for w in wins(states, k)])]


class State:
    electors = {}
    def __init__(self, code, electors):
        self.code = code
        self.electors = electors
        State.electors[code] = electors

battleground = [State('AZ', 11), State('PA', 20), State('NV', 6),
State('GA', 16), State('WI', 10), State('MI', 16)]


def is_minimal(state_codes, k):
    """Return whether a non-empty list of state_codes describes a minimal win by
    at least k.
    >>> is_minimal(['AZ', 'NV', 'GA', 'WI'], 0) # Every state is necessary
    True
    >>> is_minimal(['AZ', 'GA', 'WI'], 0) # Not a win
    False
    >>> is_minimal(['AZ', 'NV', 'PA', 'WI'], 0) # NV is not necessary
    False
    >>> is_minimal(['AZ', 'PA', 'WI'], 0) # Every state is necessary
    True
    """
    assert state_codes, 'state_codes must not be empty'
    votes_in_favor = _________
    total_possible_votes = sum(_________)
    def win_margin(n):
        "Margin of victory if n votes are in favor and the rest are against."
        return n - (total_possible_votes - n)
    if win_margin(sum(votes_in_favor)) < k:
        return False # Not a win
    in_favor_no_smallest = _________
    return win_margin(in_favor_no_smallest) < k
```



### Q11 Linked List Insertion 1⭐⭐
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018065127.png)
> 本题介绍了一种链表删除操作: `s.rest = s.rest.rest`, 需要牢记。本题介绍了一个非常重要的链表插入的思想，比如我们要在`position`处插入一段链表，那么我们可以先遍历到`position`的前一个`index`处，也就是判断条件`position > 1`的由来，如果我们的判断条件是`position > 0`， 那我们就会丧失我们要插入的`position`之前的节点信息，使得插入步骤无法进行。

```python
def replace(s, t, i, j):
    """Replace the slice of s from i to j with t.
    >>> s, t = Link(3, Link(4, Link(5, Link(6, Link(7))))), Link(0, Link(1, Link(2)))
    >>> replace(s, t, 2, 4)
    >>> print(s)
    <3, 4, 0, 1, 2, 7>
    >>> t.rest.first = 8
    >>> print(s)
    <3, 4, 0, 8, 2, 7>
    """
    assert s is not Link.empty and t is not Link.empty and i > 0 and i < j
    if i > 1:
        _________________________________________________________________________________
    else:
        for k in range(j - i):
            _______________ = ___________________________________________________________
        end = t
        while ___________________________________________________________________________:
            end = end.rest
        s.rest, end.rest = ______________________________, ______________________________


# Link ADT
class Link:
    """A linked list.

    >>> s = Link(1)
    >>> s.first
    1
    >>> s.rest is Link.empty
    True
    >>> s = Link(2, Link(3, Link(4)))
    >>> s.first = 5
    >>> s.rest.first = 6
    >>> s.rest.rest = Link.empty
    >>> s                                    # Displays the contents of repr(s)
    Link(5, Link(6))
    >>> s.rest = Link(7, Link(Link(8, Link(9))))
    >>> s
    Link(5, Link(7, Link(Link(8, Link(9)))))
    >>> print(s)                             # Prints str(s)
    <5 7 <8 9>>
    """
    empty = ()

    def __init__(self, first, rest=empty):
        assert rest is Link.empty or isinstance(rest, Link)
        self.first = first
        self.rest = rest

    def __repr__(self):
        if self.rest is not Link.empty:
            rest_repr = ', ' + repr(self.rest)
        else:
            rest_repr = ''
        return 'Link(' + repr(self.first) + rest_repr + ')'

    def __str__(self):
        string = '<'
        while self.rest is not Link.empty:
            string += str(self.first) + ' '
            self = self.rest
        return string + str(self.first) + '>'
```
```python
def replace(s, t, i, j):
    """Replace the slice of s from i to j with t.
    >>> s, t = Link(3, Link(4, Link(5, Link(6, Link(7))))), Link(0, Link(1, Link(2)))
    >>> replace(s, t, 2, 4)
    >>> print(s)
    <3, 4, 0, 1, 2, 7>
    >>> t.rest.first = 8
    >>> print(s)
    <3, 4, 0, 8, 2, 7>
    """
    assert s is not Link.empty and t is not Link.empty and i > 0 and i < j
    # 将指针s移动到index i 之前的一位
    if i > 1:
        replace(s.rest, t, i - 1, j - 1)
    else:
        # 删除 j - i 项
        for k in range(j - i):
            # 删除操作
            s.rest = s.rest.rest
        end = t
        while end.rest != Link.empty:
            end = end.rest
        s.rest, end.rest = t, s.rest
```



### Q12 Linked List Insertion 2
> ![image.png](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018069488.png)
> 本题思路如下

![](_Homework_06__Object_Oriented_Programming__Linked_Lists.assets/20230302_1018069274.png)
```python
def link_insert(lnklst, value, before):
    """Return a linked list identical to LNKLST, but with VALUE inserted just
    before the first occurrence of BEFORE in the list, if any. The returned
    list is identical to LNKLST if BEFORE does not occur in LNKLST.
    The operation is non-destructive.
    >>> L = link(2, link(3, link(7, link(1))))
    >>> print_link(L)
    (2, 3, 7, 1)
    >>> Q = link_insert(L, 19, 7)
    >>> print_link(Q)
    (2, 3, 19, 7, 1)
    >>> print_link(link_insert(L, 19, 20))
    (2, 3, 7, 1)
    """
    if _________________________________________________________________:
        return _________________________________________________________
    elif _______________________________________________________________:
        return _________________________________________________________
    else:
        return _________________________________________________________


# Link ADT
class Link:
    """A linked list.

    >>> s = Link(1)
    >>> s.first
    1
    >>> s.rest is Link.empty
    True
    >>> s = Link(2, Link(3, Link(4)))
    >>> s.first = 5
    >>> s.rest.first = 6
    >>> s.rest.rest = Link.empty
    >>> s                                    # Displays the contents of repr(s)
    Link(5, Link(6))
    >>> s.rest = Link(7, Link(Link(8, Link(9))))
    >>> s
    Link(5, Link(7, Link(Link(8, Link(9)))))
    >>> print(s)                             # Prints str(s)
    <5 7 <8 9>>
    """
    empty = ()

    def __init__(self, first, rest=empty):
        assert rest is Link.empty or isinstance(rest, Link)
        self.first = first
        self.rest = rest

    def __repr__(self):
        if self.rest is not Link.empty:
            rest_repr = ', ' + repr(self.rest)
        else:
            rest_repr = ''
        return 'Link(' + repr(self.first) + rest_repr + ')'

    def __str__(self):
        string = '<'
        while self.rest is not Link.empty:
            string += str(self.first) + ' '
            self = self.rest
        return string + str(self.first) + '>'
```
```python
def link_insert(lnklst, value, before):
    """Return a linked list identical to LNKLST, but with VALUE inserted just
    before the first occurrence of BEFORE in the list, if any. The returned
    list is identical to LNKLST if BEFORE does not occur in LNKLST.
    The operation is non-destructive.
    >>> L = link(2, link(3, link(7, link(1))))
    >>> print_link(L)
    (2, 3, 7, 1)
    >>> Q = link_insert(L, 19, 7)
    >>> print_link(Q)
    (2, 3, 19, 7, 1)
    >>> print_link(link_insert(L, 19, 20))
    (2, 3, 7, 1)
    """
    if lnklst == Link.empty:
        return lnklst
    elif lnklst.first == before:
        return Link(value, lnklst)
    else:
        return Link(lnklst.first, link_insert(lnklst.rest, value, before))

```
