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

### 8. polling refresh comonents automatically

to make the component view refresh automatically you should use `wire:poll` in the first tag of your component.
- use `keep-alive` to make it refresh in background.
- use an optional timing to add duration of refreshing. you can either use "ms" or "s" to switch between miliseconds or seconds.
```
wire:poll.keep-alive.1200ms
```

### 9. lazy loading & skeleton loading

imagine a user has a weak connection or the site has slow loading. this is very bad for your site SEO.
to do something for this, best way is lazy loading.
to setup a lazy load in the project you should go to your main view and write this in your component view location:
```
@livewire('component-view', ['lazy' => true])
```
now if there is delay in loading the website user will see a blank page before the site fully loaded. but it's still not good at all. 
**so we will use Skeleton Loading.**
we should follow these steps to make a skeleton loading:
1. find a skeleton loading template and copy the source code.
2. go to your component and make a new method before your render method. name it "skeletonLoad" or "placeholder" or ... . 
3. make a new blade name it "skeleton" or "placeholder".
4. back to your component go to your new mathod add `return view('skeleton')`.
alright you got your skeleton load now.

### 10. Live property Update

you better use live property update for search bars and live validation in forms.

you can use it by following these steps:
1. in your component use:
```
public $search;
```
in your render function use:
```
return view('your component view', [
    'user' =>  User::latest()
    ->where('name', 'like', "%{$this->search}%")
    ->paginate(),
    ]);
```
2. go to your component view add `wire:model.live='search'` to your search input.
there a potential problem that is if yo use `live` alone it will make alot of requests that may broke your website.
- you can use `live.blur` to make it search when the user clicked out of the search box.
- or you can use `live.debounce.200ms` to make it search after the user stoped typing for 200ms.
- either you can use `live.throttle.500ms` to make a interval fo searching with duration of 500ms.
thats it.

### 11. Computed property
to use computed property we should make a new method in our component then add `#[computed()]` at the top of it.
- if we passing a array data to the view we should define our foreach loop like this: `@foreach($this->method-name as $item)`

**there is two benefits for using computed properties**
1. you can have quick access to the property everywhere in project by using only: `$this->method-name`
2. you'll have more secure property and it will never show in your html page.

### 12. full page components