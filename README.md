# luamacros-documentation
Complementary documentation for the awesome https://github.com/me2d13/luamacros project. 

[![HitCount](http://hits.dwyl.io/quirinux/luamacros-documentation.svg)](http://hits.dwyl.io/quirinux/luamacros-documentation)

This page aims to help new luamacros adopters and for that ones who like to use it better as well

## What luamacros is?
Borrowed from [lumacros github repository](https://github.com/me2d13/luamacros) README page:

>This software can recognize and manage multiple keyboards connected to computer with Windows OS. This is key feature to use it as macro triggerring application. Other typical usage is for flight simulation when macro triggers can come from various sources like
>* different keyboards
>* game devices (joysticks)
>* COM interface (arduino)
>* small embeded http server
>* game simulator itself - Xplane, on variable change
>Macro action can be anything scripted in Lua language with some extensions
>* serial communication
>* xplane simulator events (commands, data ref changes)
>* http get
>* OS commands

If I could add some works I would say it is extremally handful when a second keyboard or numpad/keypad with a load or shortcuts is needed on day to day activities or while gaming.

Need an inpiration? There it go, [a video editor guy](https://github.com/TaranVH/2nd-keyboard/tree/master/LUAMACROS), not a programmer, set it up to deal with a bunch of keyboards to make his life easier.

## How to get it installed?
Easy peasy lemon squeezy:
1. Download it on [lumacros github repository](https://github.com/me2d13/luamacros) or [click here](http://www.hidmacros.eu/luamacros.zip)
2. Unzip it wherever you like, suggestion place it on the Desktop or on your Home folder
3. Double click on LuaMacros.exe
4. Grab yourself a coffee

## First run
A blank text editor should show up, let's get it a sample script to run, on the top of luamacros windows ther is a tool box, click on first icon to pick up a script to be loaded, go to the luamacros folder, inside it there is another _samples_ folder with a quickstart.lua file, choose this one to get started.
The script should be loaded on luamacros, so let's analyze it a bit:
``` lua
-- assign logical name to macro keyboard
lmc_assign_keyboard('MACROS');

-- define callback for whole device
lmc_set_handler('MACROS',function(button, direction)
  if (direction == 1) then return end  -- ignore down
  if     (button == string.byte('C')) then lmc_spawn("calc")
  elseif (button == string.byte('N')) then lmc_spawn("notepad", "C:\\test.txt")
  elseif (button == string.byte('H')) then lmc_send_keys('Hello world')
  else print('Not yet assigned: ' .. button) 
  end
end) 
```

After set it to run, clicking on run button on the toolbar luamacros will ask to assign a keyboard to be listen and triggered and them setup the shortcuts:
* C => to open the calculator program
* N => to open the notepad pagram with file placed on c:\test.txt
* H => to type down "Hello world!" text on foreground program
* everything else apart of that will be logged on luamacros main window

Easy isn't it? So let's dig in.

## Luamacros functions
The follow section describes each function avialable for lumacros to the script, just bear in mint that lua standard library functions are still avialable and a little of knowledge about lua is required but not mandatory, once it is very close to almost all fammous languages on the market, [further details here](https://www.lua.org/manual/5.3/manual.html).

### List of Functions
* [print](#print)
* [clear](#clear)
* [lmc_log_module](#lmc_log_module)
* [lmc_log_spool](#lmc_log_spool)
* [lmc_log_all](#lmc_log_all)
* [lmc_send_keys](#lmc_send_keys)
* [lmc_send_input](#lmc_send_input)
* [lmc_spawn](#lmc_spawn)
* [lmc_minimize](#lmc_minimize)
* [lmc_load](#lmc_load)
* [lmc_say](#lmc_say)
* [lmc_get_window_title](#lmc_get_window_title)
* [lmc_sleep](#lmc_sleep)
* [lmc_reset](#lmc_reset)
* [lmc_print_devices](#lmc_print_devices)
* [lmc_get_devices](#lmc_get_devices)
* [lmc_assign_keyboard](#lmc_assign_keyboard)
* [lmc_device_set_name](#lmc_device_set_name)
* [lmc_set_handler](#lmc_set_handler)
* [lmc_set_axis_handler](#lmc_set_axis_handler)
* [lmc_get_button](#lmc_get_button)
* [lmc_add_com](#lmc_add_com)
* [lmc_send_to_com](#lmc_send_to_com)
* [lmc_xpl_command](#lmc_xpl_command)
* [lmc_get_xpl_variable](#lmc_get_xpl_variable)
* [lmc_set_xpl_variable](#lmc_set_xpl_variable)
* [lmc_xpl_text](#lmc_xpl_text)
* [lmc_xpl_command_begin](#lmc_xpl_command_begin)
* [lmc_xpl_command_end](#lmc_xpl_command_end)
* [lmc_on_xpl_var_change](#lmc_on_xpl_var_change)
* [lmc_remove_xpl_var_change](#lmc_remove_xpl_var_change)
* [lmc_xpl_log](#lmc_xpl_log)
* [lmc_inc_xpl_variable](#lmc_inc_xpl_variable)
* [lmc_inc_xpl_array_variable](#lmc_inc_xpl_array_variable)
* [lmc_http_server](#lmc_http_server)
* [lmc_http_get](#lmc_http_get)
 --- 
### print
To print a string message to log console

#### Usage
```  lua
print("Hello World!")
``` 
### clear
To clear all log entries on log console 

#### Usage
``` lua
clear()
```
### lmc_log_module
### lmc_log_spool
### lmc_log_all
Enables the debug mode, sending all message logs to log console

#### Usage
``` lua
lmc_log_all()
```
Once all Luamacros messages are logged on this mode, it is a good start point to report a bug or to trace down a bad behaviour
Another side effect is the fact that it logs the keystrokes of all keyboards, so it is useful when trying to figure out some [virtua key-code](https://msdn.microsoft.com/en-us/library/windows/desktop/dd375731(v=vs.85).aspx) to remap or to trigger
### lmc_send_keys
### lmc_send_input
Enables programmatically pressing and releasing keys

#### Usage
```lua
lmc_send_input(button, 0, 0) --Presses button down
lmc_send_input(button, 0, 2) --Releases button
```

### lmc_spawn
### lmc_minimize
Minimizes the LuaMacros Window

#### Usage
```  lua
lmc_minimize()
``` 
### lmc_load
### lmc_say
Uses text to speech to audiably say the given text

#### Usage
``` lua
lmc_say("Hello World")
```

### lmc_get_window_title
To get the Application Window Title, useful to to have different behaviour on different programs

#### Usage
``` lua
lmc_get_window_title()
```

Obs:
1. Good to be set to a variable
2. Windows title doesn't mean program exe name
3. May not work with certain programs

### lmc_sleep
To make the script stops for a specific amount of time, in milliseconds

#### Usage
``` lua
lmc_sleep(1000) -- to sleep the flow for 1 second
```

### lmc_reset
### lmc_print_devices
Prints the devices that are connected to the computer

#### Usage
``` lua
lmc_print_devices()
```

### lmc_get_devices
### lmc_assign_keyboard
### lmc_device_set_name
### lmc_set_handler
### lmc_set_axis_handler
### lmc_get_button
### lmc_add_com
### lmc_send_to_com
### lmc_xpl_command
### lmc_get_xpl_variable
### lmc_set_xpl_variable
### lmc_xpl_text
### lmc_xpl_command_begin
### lmc_xpl_command_end
### lmc_on_xpl_var_change
### lmc_remove_xpl_var_change
### lmc_xpl_log
### lmc_inc_xpl_variable
### lmc_inc_xpl_array_variable
### lmc_http_server
### lmc_http_get
