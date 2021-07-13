## Unique identifier 

If you are ever in the situation of running automatic experiments or perform large scale data farming tasks in VBS4, you might want to assign unique identifiers to your units / soldiers.
The following function returns such a unique identifier in form of a string.
Please add the code to your init.sqf file.

```
// -------------------- FUNCTIONS --------------------

// Generate a unique identifier based on the current 
// time, a random number and an increasing counter.
// Parameter: None
// Return: Unique identifier as string
// Scope: public
// Example: _status = (["log message text"] call write2LogFile);  ->  writes "log message text" to file

getUniqueIdentifier = {
    _timeStr = ["YmdHisu"] call fn_vbs_dateToString;
    _rndNumber =  str (round ( random 100 ) );
    idCounter = idCounter + 1;
    ( str idCounter ) + _rndNumber + _timeStr
};

// ----------- INIT  -----------

// init identifier counter
idCounter = 0;
```

If you want to assign unique identifiers to all of your mission's soldiers, add the following lines of code also to your init.sqf file.

```    
// assign unique identifiers to all soldiers
_array = allUnits;
{
    _x setUnitName ([] call getUniqueIdentifier);
} forEach _array;

```

## Create Units
```
showShotTrajectories true;


// number of units to generate
n = 50;

for [{_i=0}, {_i<n}, {_i=_i+1}] do {

	// compute the unit position relative to the position of 
    // the object "ctr" (or whatever you want)
    _p = (getPos ctr);
    _x = _p select 0;
    _y = _p select 1;
    _z = _p select 2; 
    _up = [_x - _i, _y - _i, _z];
    
	// creates the same unit type as the player without belonging to any group
    _unit = (createGroup west) createUnit [typeOf player, _up, [], 0, "NONE"];
};


```
