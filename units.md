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

Create and position units in a circular manner around a given center.
In below example, a chain of soldiers is generated around the player's position.
<p align="center"><img alt="smoothing" src="https://github.com/armasuissewt/VBS4CodeSnippets/blob/main/rsc/snailchain.png" width="80%"></p>

```
// Generate a chain of units in a circular manner in 
// increasing distance from a given center.
// Parameter 1: number of units
// Parameter 2: a model unit (example soldier)
// Parameter 3: the center position
// Parameter 4: minimum distance from the center
// Parameter 5: maximum distance from the center
// Return: NONE
// Example: _logPath = (["dirname"] call genrateSnailChain);  ->  "dirname\\20210725111559.log"

genrateSnailChain = {

    // decompose into arguments
    _nbr        = _this select 0;
    _modelunit  = _this select 1;
    _circcenter = _this select 2;
    _mindist    = _this select 3;
    _maxdist    = _this select 4;
    
    // precompute some geometric values
    _cx = _circcenter select 0;
    _cy = _circcenter select 1;
    _cz = _circcenter select 2; 
    _dstep = (_maxdist - _mindist) / _nbr;
    _astep = round (360.0 / _nbr);

    // generate _nbr units
    for [{_i=0}, {_i<_nbr}, {_i=_i+1}] do {

        // generate current unit's distance and angle
        _d = _mindist + (_i*_dstep);
        _a = _i*_astep; 

        // compute the final unit position 
        _finalPos2D = [[_cx,_cy], _a, [_cx+_d, _cy]] call fn_vbs_rotatePoint;
        _finalPos3D = [_finalPos2D select 0, _finalPos2D select 1, _cz];

        // creates the same unit type as the "model" object without belonging to any group
        _unit = (createGroup west) createUnit [typeOf _modelunit, _finalPos3D, [], 0, "NONE"];
        _unit lookAt _circcenter;
        _unit setUnitPos "UP";
    };
};
```

The corresponding function call could be:
```
([50, player, (getPos player), 10, 50] call genrateSnailChain);
```


