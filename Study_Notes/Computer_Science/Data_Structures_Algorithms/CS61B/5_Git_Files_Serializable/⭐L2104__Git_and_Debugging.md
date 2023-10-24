[Lab 4_ Git and Debugging _ CS 61B Spring 2021.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674303741245-3ca04f2d-27ec-4f3c-89d0-7b3a96ebc55f.pdf)
# Pre-Lab
> ![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946474307.png)


# Git Intro
## Git Intro Part 1 - Commands
[Git Intro - Part 1.mp4](https://www.yuque.com/attachments/yuque/0/2023/mp4/12393765/1674472682389-43f4eb38-306e-495c-b4fe-bd30f252bbb3.mp4)
:::info
`git init`
`git add <filename>`
`git add .`
`git checkout <commit_id>`
`git status`: 查看当前`git repo`的状态。
`subl <filename>`: 使用`Sublime`文本编辑器。
`git commit -m "comment"`: 提交。
:::


## Git Intro Part 2 - Branch
[Git Intro - Part 2.mp4](https://www.yuque.com/attachments/yuque/0/2023/mp4/12393765/1674474638671-ace14e11-36c7-4274-b48c-00ee2caa1aae.mp4)
:::info
`git init`: `Enables git to track our files and perform version control`.
`git checkout <commit_id>`: 切换到某个`commit_id`的提交状态，会`change the state of repo`, 同时进入`Detached HEAD State`, 可以随意查看当前`commit`的文件状态和信息。
`git checkout master`: 切换到最近的提交状态, 会`change the state of repo`
`git log`: 查看所有的`commit`记录及`commit_id`, 可以用于后续回滚。
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946477926.png)
`HEAD`永远指向`checkout`之后的提交状态
`master`永远指向最新一次的提交状态。
图中的`commit 0 <- commit 1 <- commit 2`称为一个`git branch`
:::


## Git Intro Part 3 - Github Repo
[Git Intro - Part 3.mp4](https://www.yuque.com/attachments/yuque/0/2023/mp4/12393765/1674476080415-8db3bee7-3c94-4a5e-a3d7-5e59451450be.mp4)
:::info
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946473462.png)`origin/master`就是`github.com/Berkeley-CS61B-Student/sp21-s1906/master`, 其实就相当于远程的`URL`，用于更新`push`状态的
`master`相当于`Part 2`中的`master`, 指向最新的`commit`
`HEAD`这里没有显式，但是也存在，指向`git checkout`之后的`commit`状态。
:::


## Git Intro Part 4 - Merge Not Conflict ⭐⭐⭐
[Git Intro - Part 4.mp4](https://www.yuque.com/attachments/yuque/0/2023/mp4/12393765/1674477064289-497885ba-6597-48aa-8cb9-cf01047b462e.mp4)
:::info
假设有两个人`p1`和`p2`, 他们同时`git clone`了同一个`github remote repo`, 到本地, 如图所示:
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946473870.png)
如果`p1`进行了`git commit`操作，则`master`指针会往后移动, 指向最新的一次`commit`上:
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946486603.png)
随后`p1`进行`git push origin master`操作, `remote repo`的`master`指针和本地的`origin/master`指针同时向后移动(`同步`):
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946485093.png)
然后`p2`进行`git commit`操作, 本地`master`指针指向最新的提交`commit 2`:
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946488496.png)
如果之后`p2`也想进行`git push origin master`之前已经`push`了一个版本，则`p2`在`push`的时候会被拒绝, 原因是`remote repo`中的一些更新，在`p2`的`local repo`中没有同步:
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946488258.png)
如果要解决这个问题，`p2`需要先输入`git pull origin master`，此时`git`会查看`commit 1`和`commit 2`之间的不同，然后尝试`merge`它们:

1. 创建一个新的`branch`, 这个`branch`由`origin/master`指针指向。

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946481760.png)

2. 在原来的`branch`中追加一个新的`commit 3`, `master`指针指向它, `tracking the merged version of commit 1 and commit 2`, 本质上，如果`p1`和`p2`的修改完全没有冲突，则`commit 3`就是将`commit 1`和`commit 2`对`commit 0`的修改收集了起来:

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946484427.png)

3. 合并成一个`branch`，且保持指针各自指向的`commit`版本不变。

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946491037.png)
之后`p2`就可以使用`git push origin master`将`commit 3`同步到`remote repo`中了:
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946494663.png)
此时如果`p1`要进行`git push`, 则必须和`p2`一样，先进行`pull`:

1. 此时`p1`的本地`master`在`origin/master`的版本之前，所以我们只需要将`commit 2`和`commit 3`接在后面就可以。

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946491100.png)![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946496252.png)
:::



## Git Intro Part 5 Merge Conflict⭐⭐⭐⭐⭐
[Git Intro - Part 5.mp4](https://www.yuque.com/attachments/yuque/0/2023/mp4/12393765/1674483032653-551a1c74-e220-415b-9968-880b8c54e0d2.mp4)
:::info
如果`p1`和`p2`对同一文件的修改是冲突的，比如对相同文件的同一行进行了不同的修改，那么`git pull`在尝试`merge`的时候就不知道到底该选哪个了。此时就会报`merge conflict`的提示，让用户选择要`merge`哪个版本。我们看到下面的演示:

1. 假设这是初始的版本:

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946496612.png)

2. 现在`p2`进行了`local commit`操作, 是`commit 4`:

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946492132.png)

3. `p1`也对同一个文件进行了`commit`操作, 是`commit 5`:

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946503305.png)

4. `p2`进行了`push origin master`的操作:

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946509708.png)

5. `p1`进行`pull origin master`操作，`git`会去查看本地的`origin/master`, 然后创造一个`split branch`:

此时由于对同一个文件的同一个地方进行了修改，导致`merge conflict`的发生，比如下面的第`25`行
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946501649.png)![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946508495.png)
此时`git`会让用户进行选择要保留哪一个，是`3 * n + 1`还是`2 * n + 1`, 等待用户的选择。用户选择完毕后，`git`就会进行`merge`操作，和之前一样创建一个新的`commit 6`，然后把`branches`合并。
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946505693.png)![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946505436.png)

6. `p1`进行`git push`操作

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946515146.png)

7. `p2`进行`git pull`操作。

![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946511842.png)
:::


## Git Intro Part 6 Multi-Remote Repo
[Git Intro - Part 6.mp4](https://www.yuque.com/attachments/yuque/0/2023/mp4/12393765/1674484253560-2b7a3843-3b07-4a8c-b71f-2d30404c0308.mp4)
:::info
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946515164.png)
执行`git pull skeleton master`从左侧的`remote repo`获取数据:
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946519815.png)
在`local repo`上做一些`commit`:
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946515254.png)
然后`git push origin master`(`origin master`是另一个`repo`, 在右侧):
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946512491.png)
左侧的`repo`进行了一些更新(`commit 3`, 比如更新了一些`Projects`):
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946514782.png)
进行`git pull skeleton/master`，假设没有`merge conflict`发生，且`automatic merge`成功，则：
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946528807.png)
:::


## Summary
:::info
![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946521831.png)
:::


## Using Git Guide
[Using Git _ CS 61B Spring 2019.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674485661184-b35f9725-974b-4b2e-b2ce-8a5c0823ad91.pdf)
[Git WTFS _ CS 61B Spring 2019.pdf](https://www.yuque.com/attachments/yuque/0/2023/pdf/12393765/1674485693703-fb150046-5dbb-48f2-ac5f-8daba9af510f.pdf)



# Git Exercises
## Step 1: Merge Conflict
> ![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946522112.png)


## Step 2: Submission to Lab4A
> ![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946522678.png)


## Step 3: Detached HEAD state
> ![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946522401.png)



## Step 4: Get out of detached state
> ![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946522741.png)



## Step 5: Reverse to correct version
> ![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946527546.png)


## Step 6: Checkout a sepcific file
> ![image.png](⭐L2104__Git_and_Debugging.assets/20230302_0946529372.png)



# Debugging Mystery(Skipped)
