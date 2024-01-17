# adding a livewire to view
to adding a livewire view to a laravel blade view simply type ``@livewire('component_name')``

everything about livewire will be done in the component(the file in app/livewire)

# component commands
### 1. you can add methods similar to controller methods in the component.
you can use ``wire:click="component_method"`` to interact with the method by clicking a button or a link.

### 2. you can pass some data in view by doing: 
```
return view('view directory',compact('variable'))
```
### 3. data binding
to bind some data in DB you should follow this steps:
1. add ``public`` variables.
```
public $variable;
```
2. add ``wire:model="variable"`` to your frontend.
```
<input wire:model="variable" type="text" ...>
```
3. make a method to store records in table.
```
public function createUser()
{
    //code...
}
```
then add ``wire:submit="createUser"`` to ``form`` property to proceed binding.

### 4. validation

**validating data in livewire is very similar to how you do it in controller:**
 
 create a validate property like:
```
 $this->validate([
    'name' -> 'required|...',
    ...
 ])
```