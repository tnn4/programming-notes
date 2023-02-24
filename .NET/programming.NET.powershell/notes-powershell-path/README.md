

Changing the actual environment variables can be done by using the env: namespace / drive information. For example, this code will update the path environment variable:

``` ps
$env:Path = "SomeRandomPath";             (replaces existing path) 
$env:Path += ";SomeRandomPath"            (appends to existing path)
```
Making change permanent

There are ways to make environment settings permanent, but if you are only using them from PowerShell, it's probably a lot better to use Powershell profiles script.

Everytime a new instance of Powershell starts, it look for specific script files (named profile files) and execute them if they do exist. You can edit one of these profile to customize your enviroment.

To know where those profile scripts are located in your computer type:

``` ps
$profile                                     
$profile.AllUsersAllHosts           
$profile.AllUsersCurrentHost        
$profile.CurrentUserAllHosts    
$profile.CurrentUserCurrentHost     
```
You can edit one of them, for example, by typing:

``` ps
notepad $profile # or
code $profile # if you have vscode
```
