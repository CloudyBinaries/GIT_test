عشان اشوف التغيير اللي بين ال blob او ال Tracked object اللي في ال Working Directory و بين ال Staging Area بستخدم بس دا طبعا قبل ما اعمل ADD : 

```bash 
git diff
```

![[Pasted image 20261028023114.png]]

بعد لما اعمل Add لل file دا 
==🟣كدا ال Diff مش هيديني حاجة دلوقتي مبقاش في فرق بين ال Working Tree , Staging Area==

الفرق بين ال Index , Repo هو : 

```bash 
git diff --staged
```

![[Pasted image 20261028023859.png]]

![[Pasted image 20261028024657.png]]

لوا نا عاوزه يخليني اخد راحتي في كتابه الcomment بدل السطر الصغير اللي بكتبه 
اول حاجة لازن احدد ال text editor اللي هكتب عليه ال comment دا في ال config : 

```bash 
git config --global core.editor "code --wait" ---> in VScode

wait attribute makes the git to wait for you to type you comment and close the vscode

```

==🟡و بعد كده لو عاوز استخدم ال editor هتكب ال commit من غير ال -m== 

لو انا عاوز ال log بشكل مختصر بستخدم ال : 

```bash 
git log --oneline
```

, و ممكن اجيب ايه الل commits الخاصة ب file معين من خلال كتابة اسم ال file : 

```bash
git log --oneline file_4.txt
```

![[Pasted image 20261028030847.png]]

, ال filtration هنا علي اكتر من حاجة غير اسماء ال files بس  
ممكن يبقي user معين , brand معين و  اخر كام commit --->  [ -<num_of_commits> ]

![[Pasted image 20261028031055.png]]

------

==🔴عشان اشوف ال Commit نفسه او اللي اقصده اللي هو التعديل اللي حصل نفسه في ال commit كله و بكل ال blobs اللي فيه== : 

```bash 
git show <commit_SHA-1>
```

---
لو عاوز اعرف الفرق او التعديل اللي بين اتنين commits او بين ال working tree اللي انا فيه دلوقتي و بين commit تاني قديم : 

```bash 
git diff <commit_1>..<commit_2> -> fro different commits

git diff <commit_X>  -> for working tree and any commit 
```

![[Pasted image 20261028031758.png]]

![[Pasted image 20261028032115.png]]

----

# Note : 

## Deleting files : 

في حالة مسحت file هو فعليا مش بيتمسح من git 
دا ال Action كله ان بيكتب انك مسحت الفايل و حتي العمليه دي بتحتاج انك تعمل Staging , committing 

## Rename files : 

لو انا علمت rename لل file من ال OS علطول 
ممكن يسبب مشاكل في GIT و
و الحل هنا اني اعمل زي Linux هنا : 

```bash 
git mv old_file new_file
```

