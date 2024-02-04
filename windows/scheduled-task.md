# Setting Up a Scheduled Task to Run Python Script in Windows
In this tutorial, we'll guide you through the process of setting up a scheduled task on Windows to run a Python script using a virtual environment.

## Step 1: Create a Virtual Environment
First, let's create a virtual environment named .venv in the C:/project folder and install the necessary dependencies:

```powershell
New-Item -ItemType Directory -Path "C:\project"
cd C:/project
python -m venv .venv
.venv\Scripts\activate
pip install schedule
```

## Step 2: Create a Python Script
Next, create a Python script named main.py inside the C:/project folder with the desired functionality.

## Step 3: Deactivate the Virtual Environment
After creating the Python script, deactivate the virtual environment:

```bash
deactivate
```

## Step 4: Create a Scheduled Task
Now, let's create a scheduled task using PowerShell to run the Python script periodically:
Open PowerShell as administrator.
Run the following PowerShell commands:

```powershell
$action = New-ScheduledTaskAction -Execute "C:/project/.venv/Scripts/python.exe" -Argument "C:/project/main.py"
$trigger = New-ScheduledTaskTrigger -Once -At (Get-Date) -RepetitionInterval (New-TimeSpan -Minutes 5) -RepetitionDuration ([TimeSpan]::MaxValue)
Register-ScheduledTask -Action $action -Trigger $trigger -TaskName "MyPythonTask" -Description "Runs main.py located in virtual environment every 5 minutes"
```

This will create a scheduled task named "MyPythonTask" that runs python.exe with the main.py script every 5 minutes, using the Python interpreter from the virtual environment located in C:/project/.venv.