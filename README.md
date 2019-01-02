# PowerShell_to_Python

## Wednesday January 02, 2019

PS C:\Users\tcailleau\Documents\Python\PowerShell_to_Python> C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe .\Identation.ps1 
Hello Thierry! 
PS C:\Users\tcailleau\Documents\Python\PowerShell_to_Python> C:\ProgramData\Anaconda3\python370.exe .\Identation.py 
Hello Thierry! 
PS C:\Users\tcailleau\Documents\Python\PowerShell_to_Python> 

## Sunday December 16, 2018

vscode version:

-----------------

Version: 1.30.0 (user setup)
Commit: c6e592b2b5770e40a98cb9c2715a8ef89aec3d74
Date: 2018-12-11T22:29:11.253Z
Electron: 2.0.12
Chrome: 61.0.3163.100
Node.js: 8.9.3
V8: 6.1.534.41
OS: Windows_NT x64 10.0.15063

-----------------

I figured how to make default to PS by ignoring the message "always"

I also had to rename those files to make the debugger work too:
C:\ProgramData\Anaconda3\python370.exe
C:\ProgramData\Anaconda3\pythonw370.exe
C:\ProgramData\Anaconda3\pythonw370.pdb

Which then returns for "Case1.py" (in the debugger mode, i.e. with the "locals" variables)

-----------------

PS C:\Users\tcailleau\Documents\Python\PowerShell_to_Python> cd 'c:\Users\tcailleau\Documents\Python\PowerShell_to_Python'; ${env:PYTHONIOENCODING}='UTF-8'; ${env:PYTHONUNBUFFERED}='1'; & 'C:\ProgramData\Anaconda3\python370.exe' 'c:\Users\tcailleau\.vscode\extensions\ms-python.python-2018.12.1\pythonFiles\ptvsd_launcher.py' '--default' '--client' '--host' 'localhost' '--port' '51461' 'c:\Users\tcailleau\Documents\Python\PowerShell_to_Python\Case1.py'
Thierry
Cailleau

and in a separate debug window:

Exception has occurred: NameError
name 'Print' is not defined
  File "C:\Users\tcailleau\Documents\Python\PowerShell_to_Python\Case1.py", line 5, in \<module>
    Print(name)

-----------------

## Sunday December 09, 2018

I re-installed vscode on 12/09/2018 to have it automatically installed necessary Python plugin and configuration's files, following some good tip from this video from Alan Simpson:
<https://www.youtube.com/watch?v=g-aS9oVY-DA>

Turns out beside installing 3 plugins [Python (Windows), Anaconda Extension Pack, YAML Support by Red Hat], Anaconda's install of vscode also adds the following 2 lines to the "User Settings" file located here (for me):

C:\Users\tcailleau\AppData\Roaming\Code\User\settings.json

    ],
    "python.pythonPath": "C:\\ProgramData\\Anaconda3\\pythonw.exe",
    "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\cmd.exe"
}

This made me realize that:

1. Adding the path to "powershell.exe" allows it to run with Powershell without the message "Activation of the selected Python environment is not supported".... ..."Use Command Prompt"

2. Changing "python.pythonPath" to point to python.exe instead of pythonw.exe display the result in the PowerShell prompt as expected. Note: I renamed the executable python.exe to python370.exe to help document my examples this was run using Python 3.7.0

    ],
    "python.pythonPath": "C:\\ProgramData\\Anaconda3\\python370.exe",
    "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\WindowsPowerShell\\v1.0\\powershell.exe",
    "terminal.integrated.shell.windows": "C:\\WINDOWS\\System32\\cmd.exe"
}

I also found out there is another "User Settings" file located here (for this project):

C:\Users\tcailleau\Documents\Python\PowerShell_to_Python\.vscode\settings.json

It only had this entry:

{
    "python.pythonPath": "C:\\ProgramData\\Anaconda3\\python.exe"
}

Which I need to modify to:

{
    "python.pythonPath": "C:\\ProgramData\\Anaconda3\\python370.exe"
}

Running the first Case1.py with cmd.exe (earlier attempt) in this repository returns this (note: I edited the mistake I made and I am only showing what it should have returned to start with):

-----------------

Microsoft Windows [Version 10.0.15063]
(c) 2017 Microsoft Corporation. All rights reserved.

C:\Users\tcailleau\Documents\Python\PowerShell_to_Python>C:\ProgramData\Anaconda3\Scripts\activate base

(base) C:\Users\tcailleau\Documents\Python\PowerShell_to_Python>C:/ProgramData/Anaconda3/python370.exe c:/Users/tcailleau/Documents/Python/PowerShell_to_Python/Case1.py
Thierry
Cailleau
Traceback (most recent call last):
  File "c:/Users/tcailleau/Documents/Python/PowerShell_to_Python/Case1.py", line 5, in \<module>
    Print(name)
NameError: name 'Print' is not defined

(base) C:\Users\tcailleau\Documents\Python\PowerShell_to_Python>

-----------------

I also somehow managed run Python from PowerShell (with error message "Activation of the selected python environment is not supported"), but restarting vscode brings me back to the cmd.exe for Python every time.

Running the first Case1.py in this repository returns this:

-----------------

Windows PowerShell
Copyright (C) 2016 Microsoft Corporation. All rights reserved.

PS C:\Users\tcailleau\Documents\Python\PowerShell_to_Python> & C:/ProgramData/Anaconda3/python370.exe c:/Users/tcailleau/Documents/Python/PowerShell_to_Python/Case1.py
Thierry
Cailleau
Traceback (most recent call last):
  File "c:/Users/tcailleau/Documents/Python/PowerShell_to_Python/Case1.py", line 5, in \<module>
    Print(name)
NameError: name 'Print' is not defined
PS C:\Users\tcailleau\Documents\Python\PowerShell_to_Python>

-----------------
