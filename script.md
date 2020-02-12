# CI-Simulator Script editing guide
This page explains about scripts used on CI-Simulator

## Types of Scripts
### Map init script
Map init script is script that is initiated when map is started. It only executes once.
### Map step script
Map step script is script that is executed one line per one frame. Map script always executed first than any other instance's script.
### Inst init script
Inst script is script that is initiated when map is started. It only executes once.
### Inst step script
Inst step script is script that is executed one line per one frame. If the id of the  

## Variables / registers
There some built-in variables and registers that is available
### Map variables
Map has its own built-in variables. These are not editable with code
 - ```num_inst``` : number of instances
 - ```time``` : time passed from start of the room
 - ```width```: width of the room
 - ```height```: height of the room

### Map registers
Map can have total of 8 float registers

### Inst Constants
Each instance has its own built-in constances.

### Inst variables
Each instance has its own built-in variables.
 - ```x```: (float) Instance's current x position
 - ```y```: (float) Instance's current y position
 - ```id```: (int) Instance's id
 - ```tag```: (string) Instance's tag
 - ```class```: (string) Instances' class
 - ```type```: (string) Instance's type
 - ```enable```: (bool) ```true``` if instance is activated. Set to ```false``` to deactivate object
 - ```visible```: (bool) ```true``` if user want this object is visible. Not visible instances is not always deactivated.
 - ```speed```: (float) Current speed of the instance

### Inst registers
There are total of 8 float instance registers available to each instances. They are accessable with ```r0, r1, r2, r3, r4, r5, r6, r7```

## Comments
 - Use ```self``` to use self's variables
 - Classes: Object / Effect / Background

## Commands (Avaiable places)
### Common
#### set
```set [var/reg] [value or var/reg]```: Set the specific variables.
```set [var/reg] [value or var/reg] [operator] [value or var/reg]```: Set the specific variables.
 - ```set r0 3``` set this instances's r0 register to 3.0
 - ```set r0 r0 + r1``` set this instances's r0 register to r0 and r1's addition
 - operators: + - / //(int divide) * %
#### tag
```tag [name]```: set the tag name used on jump position. Tag shouldn't start with number.
 - ```tag loops``` set the current position as ``loops```
#### move
```move [value] [value]```: move to x,y coordinate with this instance's speed. Command pointer will not pass through until this command is fully executed.
 - ```move 5 11```: move this object to (5,11)
#### end
```end```: end the commands. if this is not at end of the script, command executes from first line again(!)

### Condition
#### if
```if [value or inst.var/reg] [comparator] [value or inst.var/reg] [jump position]```: if 
 - ```if self.r0 > 3 loop```: if current instance's r0 register is bigger than 3, then jump to loop position, otherwise, proceeds to next line.
 - ```if self.x <= 24.x +10```: if current instance's x value is smaller or same than instance id 24's x value, execute 10 line forward from line that should execute next.
 - ```if time > 4.3 22```: if map time is bigger than 
 - available comparator: >, >=, <, <=, ==
#### jump
``` jump [jump position]```: jump to jump location

### Only useable on object.client
List of action works like priority list with index is priority. Index doesn't need to start from 0, but game will find smallest index, and execute

Actually, now I'm thinking about way the acting works to use with this only command of ```act``` which command pointer doesn't moves while client acting.
#### act add
```act set [index] [action] [duration]```: set action to the instance
 - ```act add 0 right 2``` set this object's action index 0 to move right for 2 seconds
 - Available keyword for action: idle, right, left, jump, jumpr, jumpl, crouch, power
#### act remove
```act remove [index]```: remove index of the action. if index is not set, remove the last one. If index is ```all```, then remove all action
#### act restart
```act restart```: restart act from start

### Misc
#### Comments
```//``` to make comments
