## Key Event Handler
Following code is registering a key listener. Depending on the pressed code, an external script with different parameters is called. In this example the keys H and J are captured.

```
// -------------------- init.sqf --------------------

// ascii key codes
h_key_ascii_code = 35;
j_key_ascii_code = 36;

// main screen has id 46
waitUntil { !isNull findDisplay 46 };
(findDisplay 46) displayAddEventHandler [ 
  "keyDown", 
   "
        key_pressed = _this select 1;
        if (key_pressed == h_key_ascii_code) then {  
            ['H Key pressed', player] execVM 'myfunc.sqf';
        } elseif (key_pressed == j_key_ascii_code) then {
		    ['J Key pressed', player] execVM 'myfunc.sqf';
		} else {
            hint str key_pressed;
        }
   " 
];
```

```
// ----------------- myfunc.sqf ----------------------
params ["_msg", "_unit"];
_unit groupChat _msg;
hint _msg;
```

