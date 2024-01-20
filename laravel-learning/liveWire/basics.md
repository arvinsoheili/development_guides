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

you should reset your input fields after form submitted. to do this simply add `$this->reset('name', ...)` at the end of your create method.

### 5. flash massages

after user submit a form there should be a massage to alert success to the.

1. go to your component add the code below at the end of your create method:
```
$this->session()->flash('success', 'created successfully');
```
2. go to the view add:
```
@if(session('success'))
    {{ session('success') }}//its better to give some style to it
@endif
```
### 6. pagination

to use livewire pagination follow these steps:
1. go to component location, use: `$users = user::paginate(int: items per page)`, instead of: `$users = user::all()`
2. add `use WithPagination;` before all of the methods.
3. go to the view and implement `{{ $user->links() }}`

- you can switch to bootstrap by publishing livewire config(`php artisan livewire:publish --config`), then open config file location: `config/livewire`. head to "pagination-theme" and change the theme.

- also you can use custom templates for pagination. first use `php artisan livewire:publish --pagination`. then you can access pagination views in the view dir and you should reference the view in `{{ $users->links('vendor.livewire.custom-theme) }}`

### 7. events
we have two seprate components like: one of them for creating user, and the other is for display it.how we can do somthing that when our new user created we can see it in list.
1. for the first component we should use the code below in the create method:
```
$this->dispatch('user-created', $variable-that-you-use-for-create);
```
2. now go to your 2nd component create new method named like updateUser and use this anotation at the top of the function:
   ```
   use LiveWire\Attributes\On; //use this after namespaces
   #[On('user-created')]
   ```
- optionally you can use the code on the "render" method. 


   
