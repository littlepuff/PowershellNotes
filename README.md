# NOTES ![build status](https://ci.appveyor.com/api/projects/status/github/JRJurman/PowerLS?svg=true&retina=true) 
## **foreach, where and select**
### 1._foreach:_
```powershell
1..10|foreach {echo "hello $($_)"}
```
when refer a variable in a string ,use $() 2. 1..10 means every number from 1 to 10

### 2._select&where:_
```powershell
dir|select name,length,@{n=$_.cpu;e='myCPU'}
dir |sort name|select -last 5
```
1.choose the attributes to show in the screen(use argu property)
2.choose objects based on order
```powershell
dir| where name -match '*.exe'
dir| where {$_.name -match '*.exe'}
```
choose objects based on attributes
1. use the -property
2. use the -filterscript
## **use of backgroound(job)**
### 1._start-job_
```powershell
start-job -Initial {$v='*.py'} -ScriptBlock {dir -name $v}
start-job -filepath E:\emacs.ps1 -argumentlist $pwd.path,python.py
{
$script= [scriptblock]::Create("emacs E:\python.py")
start-job -ScriptBlock $script 
}
```
3 ways to pass variables to start-job.
1. initial
2. argumentlist
3. a [scriptblock] type varaible(varaibles created before start-job can be passed through such a variable )

### 2._receive-job_
```powershell
$job=start-job
receive-job $job
```

## **use of arguments in function**
### 1._万能参数$args_
```powershell
function sayHello
{
    if($args.Count -eq 0)
    {
        "No argument!"
    }
    else
    {
        $args | foreach {"Hello,$($_)"}
    }
}
```

