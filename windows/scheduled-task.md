# Setting Up a Scheduled Task to Run a Python project in Windows
In this tutorial, we'll guide you through the process of setting up a scheduled task on Windows to run a Python script using a virtual environment.

## Step 1: Create a Virtual Environment
First, let's create a virtual environment named .venv in the C:/project folder and install the necessary dependencies:

```powershell
New-Item -ItemType Directory -Path "C:\project"
cd C:/project
python -m venv .venv
.venv\Scripts\activate
```

## Step 2: Create a Python Script
Next, create a Python script named main.py inside the C:/project folder with the desired functionality. Example

```powershell
# Create main.py file with specified content
@"
import time

print('This is my first task!')
time.sleep(300)  # Wait for 5 minutes
"@ | Out-File -FilePath "C:\project\main.py" -Encoding utf8
```


## Step 3: Deactivate the Virtual Environment
After creating the Python script, deactivate the virtual environment:

```powershell
deactivate
```

## Step 4: Create a Scheduled Task
Now, let's create a scheduled task using PowerShell to run the Python script periodically:
Open PowerShell as administrator.
Run the following PowerShell commands:

```powershell
New-ScheduledTaskAction -Execute "C:/project/.venv/Scripts/python.exe" -Argument "C:/project/main.py" -WorkingDirectory "C:/project/"
```

```powershell
$trigger = New-ScheduledTaskTrigger -Weekly -DaysOfWeek  Monday, Tuesday, Wednesday, Thursday, Friday -At 10am
```

```powershell
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "MyPythonTask" -Description "Runs python project from Monday to Friday at 10am"
```

This will create a scheduled task named "MyPythonTask" that runs python.exe with the main.py script every 5 minutes, using the Python interpreter from the virtual environment located in C:/project/.venv.

## Conclusion
You can edit your new scheduled task using the Windows TaskManager.exe at `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Administrative Tools`.

For additional information on using Powershell commands to create scheduled tasks, visit https://learn.microsoft.com/en-us/powershell/module/scheduledtasks/?view=windowsserver2022-ps