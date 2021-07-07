## Dynamic log file generation 
In VBS4, there exist various methods to print messages to the screen (<code>hint</code>, <code>sidechat</code>, ...) or write them into the general mission's log file (<code>VBS_addEvent</code>).
As a developer, however, it is often practical to have your own permanent storage where you can keep whatever information you want to.
The little code snippet below creates a new custom log file whenever a mission is started.
The log file name is generated based on the current date and time.
Please copy this code to your mission's init.sqf file.

```
// Generates a log file path based on the given directory and the current time and date.
// Parameter: The directory as string
// Return: Generated log file path as string
// Example:  _logPath = (["dirname"] call _getNewLogFilePath); -> "dirname\\20210725111559.log"

_getNewLogFilePath = {
    _directory = _this select 0;
    _timestr = ["YmdHis"] call fn_vbs_dateToString;
    _directory + "\\" + _timestr + ".log"
};



```
