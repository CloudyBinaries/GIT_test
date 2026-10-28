
==🔴عشان نعمل Initialization لل Git Environment==  
بندخلي علي ال Root و اللي بعد كده بيبقي اسمه ال Master 
بتاع المسار اللي هنبدأ شغل فيه و نكتب : 

```bash
git init
```

, و بمجرد اننا ننفذ الامر دا كدا ال Working directory بتعنا ل Git Repo , و بيبقي جواه : 

```text
.git    ---->  git structure
    |- ..
    |- branches
    |- config [f]
    |- description [f]
    |- HEAD [f]
    |- hooks
    |- info
    |- objects
    |- refs
```

-----

لل Configuration ل Git 
, واحده من الحاجات دي هي انك تدي اسمك و ايميلك ل GIT 
==🟡عشان و هو بيسجل ال Action يسجل مين اللي عملهم و عملهم امتي في ال Git Logs==
==🟡, و دا جزء من عملية ال Tracking== 

```bash
git config --global user.name "Ahmed Atef"
```

```bash
git config --global user.email "ahmedatef11115114@gmail.com"
```

, و كلمة global هي بالنسبة لل user - اما بقي بالنسبة لكل حاجة و كل ال Users بنستخدم :

```bash 
git config --system
```

لو عاوز تشوف ال Configuration اللي عملتها : 

```bash 
git config --list
```

------
