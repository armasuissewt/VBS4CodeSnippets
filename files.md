## Dynamic log file generation 
In VBS4, there exist various methods to print messages to the screen (<code>hint</code>, <code>sidechat</code>, ...) or write them into the general mission's log file (<code>VBS_addEvent</code>).
As a developer, however, it is often practical to have your own permanent storage where you can keep whatever information you want to.
The little code snippet below creates a new custom log file whenever a mission is started.
The log file name is generated based on the current date and time.
Please copy this code to your mission's init.sqf file.

```
// -------------------- FUNCTIONS --------------------


// Generates a log file path based on the given directory and the current time and date.
// Parameter: The directory as string
// Return: Generated log file path as string
// Scope: private
// Example: _logPath = (["dirname"] call _getNewLogFilePath);  ->  "dirname\\20210725111559.log"

_getNewLogFilePath = {
    _directory = _this select 0;
    _timeStr = ["YmdHis"] call fn_vbs_dateToString;
    _directory + "\\" + _timeStr + ".log"
};


// Writes the given line of text to the log file. The current used
// log file path is defined by the global variable logFilePath.
// Parameter: Log message as string
// Return: File operation status
// Scope: public
// Example: _status = (["log message text"] call write2LogFile);  ->  writes "log message text" to file

write2LogFile = {
    _logStr = _this select 0;
    pluginFunction ["VBSPluginFileAccess","AppendLine(" + logFilePath + ")@" + _logStr ]
};


// Writes the actual mission time [s] and a given line of text  
// to the log file. The current used log file path is defined 
// by the global variable logFilePath.
// Parameter: Log message as string
// Return: File operation status
// Scope: public
// Example: _status = (["log message text"] call write2LogFile);  ->  writes "log message text" to file

logMsg = {
    _logStr = (str time) + ", " + (_this select 0);
    [_logStr] call write2LogFile
};


// ----------- INIT (prepare log file at mission start) -----------

// log directory
_dirName = "MyLogs";  
_status = pluginFunction ["VBSPluginFileAccess","CreateDir(" + _dirName + ")"];

// note: logFilePath is a global variable
logFilePath = ([_dirName] call _getNewLogFilePath);

// write first log file entries
_status = (["Log file start"] call write2LogFile);
_status = (["Message with time stamp"] call logMsg);
```

Within your VBS4 mission, you can call from everywhere the public functions <code>logMsg</code> and <code>write2LogFile</code> to add text to the current mission's log file.
Following example logs the name of a unit which activates a trigger (insert the line into On Activate).

```    
_status = ([(str (thislist select 0)) + " activated trigger"] call logMsg); 
```
