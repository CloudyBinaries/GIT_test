
 طبيعة الشغل بتعتمد علي اننا عارفين ال Files اللي عندنا ايه حالتها و اللي هي : 

- Tracked
- Untracked
- Modified
- Unmodified

عشان نعرف الحالة دي : 

```bash 
git status    -- [ must be in the master ]
```

![[Pasted image 20261027152747.png]]

, في المثال دا جابلي ال Files ال untracked اللي عندي "هو مفيش غيره اصلا"
و في السطر اللي بعده بيقترح عليا اقتراحات بناء علي الحالة اللي فيها ال file دا 

و هو هنا بيقولي اعمله ADD عشان يبقي يتعمله Indexing في ال Staging Area [to be tracked]

- طب لو نا عاوز اشوف ال files اللي معمولها indexing in staging area : 

```bash 
git ls-files
```

- لو عاوز اشوف ايه ال Versions اللي اتكريتت في ال repo : 

```bash 
find /.git/objects/ -type f
```


![[Pasted image 20261027153331.png]]

, و بعد تنفيذ الامر دا مش هلاقي حاجة لان ببساطه مفيش حاجة لسه معملولها Tracking 

### Note : [هو احنا ليه كل شويه عاوزين نعمل ال tracking ?]

الفكرة هنا ايه اللي بيحصل لما نعمل لل file دا او حتي مجموع ال files دي Tracking , و هي 
انه ال staging area بتعملها blob فيها و في ال repo و ال repo دا عامتا ال final destination  
الفكرة ان هنا ساعة ال File ما يتعمله tracking ال staging area من خلال ال Version اللي عندها بتبدأ تقارن بينها و بين ال file نفسه و ال blob اللي هو عمله create في ال repo 
قبل ما يحصل اي تعديل في ال file يبقي ال file `unmodified`
او لما تغير اي حاجة حتي لو تافهة بيبتدي ان ال file في ال modified باللون الاحمر و دا معناه ان ال file دا مختلف عن ال version اللي في ال [ staging area - repo ] بعد ما تضيفة تاني في ال staging area بيديني Modified بس بالاخضر و دا معناه ان ال Version اللي [ repo ] بس هي اللي مختلفة عنهم الاتنين 
او ما تعمل Commit بيرجع تاني unmodified 

لو عاوز اضيف ال file لل Staging area : 

```bash 
git add file.txt
```

, بالمناسه انا ممكن اضيف العدد اللي عاوزه من ال files و ممكن كمان استعمل ال Wildcards * 
يعني : 

```bash 
git add file_1.txt file_2.txt file_3.txt 

or 

git add *.txt

or 

git add *
```

![[Pasted image 20261027155445.png]]

, و فعلا لو روحت دلوقتي علي ال index اشوف ايه اللي جوا هلاقيه version من ال file دا 

![[Pasted image 20261027214135.png]]

لو انا عاوز اشوف مش بس ال file بس 
لا انا عاوز اشوف كمان ال SHA-1 بتاعه 

```bash
git ls-file -s
```

![[Pasted image 20261027214236.png]]

اول حاجة دا نوع ال file و ال permissions اللي عليه [ create mode ] , و التانية ال SHA-1 بتاعه و اللي بتتحدد من خلال ال [ type - size - null - content ] 

, و لو روحنا لل repo tree هنلاقي : 

![[Pasted image 20261027214603.png]]

و لو لاحظت هتلاقي  ان اسمه ال folder اللي فيه ال project دا هو اول 2 characters من ال SHA-1 بتاع ال Blob و اسم ال Object نفسه باقي ال SHA-1 

لو انا عاوز اقرأ المحتوي بتاع ال Object دا [ type - size - content ] - ==🔴و اللي بالمناسبه بنقرأها بالامردا عشان Git مخلية ال files دي comprised== 
في عندي طريقة و هي : 

```bash 
git cat-file -t <SHA-1_of_object>  ---> reads the [ type ]

git cat-file -s <SHA-1_of_object>  ---> reads the [ size ]

git cat-file -p <SHA-1_of_object>  ---> reads the [ content ]
```

==🟢هل مع كل اللي احنا شوفناه== 
==🟢هل دلوقتي نقدر نقول ان Git عمل Version لل file دا في ال Git Repo== 
==🟢الاجابة هي لأ== 
==🟢اللي حصل دلوقتي و ال Object اللي موجود دا عبارة عن جزء من ال Tracking للاختلاف اللي بيحصل لل file الاصلي و اللي في ال index== 

### ==🔴Commit==   :(^ __ ^): 

```bash
git commit -m "Initail commit"
```

ال -m هنا عشان اسم زي comment علي Commit دا يعرفني بس هو دا بيعمل ايه او عامل زي Label ليه 

![[Pasted image 20261027220104.png]]

لما نيجي نشوف ال objects اللي موجوده في ال Repo هلاقي : 

![[Pasted image 20261027220233.png]]

, ==🔴و السؤال هنا : هما ليه تلاته Objects ل file واحد اتعمله commit ؟== 

![[Pasted image 20261028002855.png]]

في الرسمة دي بيان ايه هما ال 3 objects  اللي اتضافو في ال repo و اللي هما : 
- committed blob
- tree
- commit 
طب ايه ليه برضو , 
الفكرة هنا اني لما باجي اعمل commit ل blob , tree او مجموعة blobs 
او اي حاجة عامتا ال GIT بيعمل حاجة زي ==🔵Wrapper== لل tree , Blobs و للي هنا بيبقي ال commit object و اللي بدوره بيبقي شايل عنوان لل commit اللي قبله , و ال SHA-1 بتاعت ال Tree اللي بتشاور علي ال objects اللي اتعملها commit اصلا 
و الكلام دا بيوضح في المثال التالي : 

احنا هنا عاوزين نشوف ايه ال commits اللي اتعملت : 

![[Pasted image 20261028004552.png]]

هنقرأ محتوي اخر commit object و اللي هنا هنلاقيه شايل ال previous commit و اللي بيبقي اسمها parent و ال tree SHA-1

![[Pasted image 20261028005145.png]]

و نشوف بعد كده محتوي ال tree اللي شايل ال references لل committed objects 

![[Pasted image 20261028005308.png]]

و هنا بنستنتج اننا نقدر اي commit بعد كده هيتعمل هيتكون من 3 حاجات , و هما : 

- Commit objects : [ points to "previous commit" - "tree" ]
- Tree : [ points to committed objects ]
- Committed objects [ as much as commit blobs or any thing ]

==🟡الفكرة ان الطريقة دي معموله كدا لان ال Data Structure اللي بتستخدمها ال GIT في الكلام دا هي [ Linked List ]==

انا هنا عملت فايل جديد اسمه File_3 ,  و عملتله ADD و Commit لوحده , و لما دخلت في ال Tree لقيت انه في snapshot كامل لل project او Version جديد من ال project -- [ 3 files ]

![[Pasted image 20261028011601.png]]

![[Pasted image 20261028011711.png]]

![[Pasted image 20261028011735.png]]

==🔴اهو الشكلين اللي فوق في الصورة و ال CMD دول [ مجموعة ال Commits اللي بيشاورو علي بعض  ] دول علي بعض عبارة عن اللي ما يسمي بال== ==🟢Branch== 
==🟡, و اللي by default اسمه Master== 

----

### HEAD 

![[Pasted image 20261028012508.png]]

خلينا نعرف ان ال version اللي ببقي شغال عليها في ال Working Tree هي ال Version بتاعت اخر Commit في ال Get repo و دا By Default ليه بقي 
لان في زي Pointer بيشاور علي اخر Commit -- بيبقي اسمها ال ==🔴HEAD==  عامل زي ال Head بتاع شريط الفيديو اللي بحركة علي حسب انا عاوز الفيديو يشتغل علي انهي دقيقة انهي Frame 
طب في حالة اني غيرت ال HEAD دي خليتها علي Version تانية 
هلاقي ان ال Working Tree كلها اتغيرت بقت علي ال Version اللي خليت ال HEAD تشاور عليها. 

