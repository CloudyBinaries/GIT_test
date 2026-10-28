لما نتكلم عن الشكل العادي لبيئة العمل اللي علي الجهاز هنسميها حاجة [ Working Directory] او [Working Tree]

![[Pasted image 20251201064658.png]]

, و انت انشانت فيه file اسمه a.txt و عدلت فيه , هيفضل برضو a.txt و او بمعني تاني انت هتشوف في الظروف العاديه [ من غير استخدام اي شكل من اشكال ال Version Control ] في ال working directory  دا اخر حاجة انت عملتها و هيبان علي الشكل من بره انك مش عارف في حاجة هنا اتعدلت و لا لأ

#### في [ Git environment ]
![[Pasted image 20251201065259.png]]

هنا ال [ Working Tree ] بقي اسمه ال [ Git Repository ] او بنختصره و نقول عليه Repo 
و الفكرة هنا بمنتهي الاختصار انه او عدلت في a.txt اللي انت كنت عامله هيظهر انك عدلته و يبقي 
[ Version جديده ]
مثلا من [ a.txt v1.0 ] ---->[a.txt v1.1]


---------------

ايه الحاجات بنعملها Architecture يبقي ليها شوية requirements

 , و ال requirements هي ال 
1 - Track everything ( Content , metadata )
2 - OS independent ( Portable )
3 - Unique ID ( for every object )
4 - Track history 
5 - No Content Change ( don't change anything while tracking )

 بس قبل دا احنا محتاجين نعرف ان في حاجة اسمها ال [ Git Objects ]
 
1 - ال Blob (دا كان قبل كدا ال  File العادي بس بال content , metadata بتاعتو )
2 - ال Tree ( دا كان قبل كدا ال Folder بس بال content , metadata بتاعو )
3- ال Commit
4 - ال Tagged Annotations 

طب احنا عاوزين لما نيجي نعمل تتبع لأي object موجود اعنا عاوزين نراقب ال ( Content , Metadata ) , و الموضوع يبقي عبارة عن simple folder  و قابل للقراءة علي اي OS مش زي حاجة لتخزين البيانات برضو و فيها شوية tracking يرضو زي ال logs زي ال Database محتاجة config معينه علي كل OS 
معلومة ان ال [ Git repo بيبقي عبارة عن ملف مخفي جوا ال Working Tree اصلا ] , و دا كل بيتحول اسمه الي Repo , و ال Repo دا لما تيجي تعدل عليه , تنشأه من جديد , تنقله من حته لحته , من النت لجهازك , من جهاز لجهاز تاني, واحد شغال ب windows , و التاني شغال ب Linux .........
كل دا بيستخدم نفس الاوامر و بيقراء نفس الحاجات فعلشان كده هو OS independent 


احنا اتفقنا ان المسميات في ال Git مش هتبقي file , folder , والكلام دا 
بقي عندنا blob , tree
, ==🔵و اساميهم مش هتبقي identifier  -- باعتبار ان الاسم انا ممكن اغيره اصلا , فا دي مش حاجة يعتمد عليها== 
, فانا دلوقتي محتاج identifier عشان ابقي عارف ان ال file دا مين و فين و تبع انهي حاجة 
و ال identifier دا ممكن يتعمل باكتر من طريقة 
واحده منهم انك تعمل Modul في Git و تخليه يعمل [ Hash Function ] و دا عشان يعمل Unique ID
بس ال hashing المرتبط ب Git مختلف شوية عن ال hashing بتاع العادي اللي ممكن تستخدمه زي ال shasum كده مثلا في Linux
الفكرة هنا ان Git بيزود شوية حاجات من عنده زي نوع ال Object و حجمة و null
زي ما هو باين هنا :

![[Pasted image 20251201075557.png]]
و دي بتبقي حتي نفس الطريقة اللي بتعرفه اذا كان ال object دا حصل فيه تغيير , وتسجل دا في ال [  Tracking History ]  لأ اي تغير بيسبب تغير كاااااامل في ال Hash

-------------------

### Version Control System Architecture 


##### 2-tree Arch
دي و دا كانت في الانظمة القديمة من ال VCS 

![[Pasted image 20251201080258.png]]

و كان نظامها عبارة عن انك بتشتغل في ال Working Tree بتاعتك عادي و بعد كده تروح تشحنها علطول في ال Repo tree 

### بس Git مش بيتسخدم الكلام دا 

#### 3-tree Arch

![[Pasted image 20251201081653.png]]

هما ال Git اضافة tree جديد اسمه ال [ Staging Area ] او [ index ]
و وظيفة الطبقة دي باختصار انها بتهيأ حاجة قبل ما يتعملها [ commit ]
, و حتي في حاجات زي ال patch مثلا بدل ما افضل اعمل حاجة زي اني اعمل علي كل ملف هيحصله تعديل  add , commit  لا انت بتضيف الملفات اللي عاوز تعدلها و تبعتهم commit مرة واحده و ينزل دا كله علي انه تعديل واحد
و مهم برضو في حاجة زي ال [ Trouble shotting ] و اني مثلا عادي ارجع ل version قديمة و تعاملها restore 

فابختصار دي بيئة تهيئة 
و برضو عشان حاجة مهمة ان ال Working Tree دي بتبقي مش مكان عشوائي 
ممكن يبقي الproject الفعلي اللي بشتغل عليه و هيطلع للناس 
فاهنا ال [ Staging area ] دا مكان بيديني مساحة اني اشوف الفروقات و اخد القرار 


