> [https://cs61a.org/proj/hog/](https://cs61a.org/proj/hog/)

[hog.zip](https://www.yuque.com/attachments/yuque/0/2022/zip/12393765/1672307655686-d1b06ceb-b6a0-4cd1-b474-bb9568599863.zip)
[hog.pdf](https://www.yuque.com/attachments/yuque/0/2022/pdf/12393765/1672308255762-f0f7bd16-650c-4263-9cb2-12296ebca890.pdf)



# Counter Using Closure
```python
def make_test_dice(*outcomes):
    """Return a die that cycles deterministically through OUTCOMES.

    >>> dice = make_test_dice(1, 2, 3)
    >>> dice()
    1
    >>> dice()
    2
    >>> dice()
    3
    >>> dice()
    1
    >>> dice()
    2

    This function uses Python syntax/techniques not yet covered in this course.
    The best way to understand it is by reading the documentation and examples.
    """
    assert len(outcomes) > 0, 'You must supply outcomes to make_test_dice'
    for o in outcomes:
        assert type(o) == int and o >= 1, 'Outcome is not a positive integer'

    # Very useful techniques called closure, which can be used to create a counter.
	# Get incremented each time the dice() is called.
    index = len(outcomes) - 1

    def dice():
        # update the index in the closure
        nonlocal index
        index = (index + 1) % len(outcomes)
        return outcomes[index]
    return dice
```
