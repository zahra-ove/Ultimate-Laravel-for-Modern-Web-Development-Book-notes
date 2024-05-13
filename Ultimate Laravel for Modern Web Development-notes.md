## Ultimate Laravel for Modern Web Development Book Notes:

1. The two ways in which the IoC container
   can resolve dependencies are Closure callbacks and automatic resolution. (p.26)

2. It is also a good practice to configure a fallback language. This should be
   configured in the config/app.php configuration file.
   The syntax to set a fallback language is as follows:
   `falback_locale` => `<language>`\
   An example, to set the fallback language as English:\
   `falback_locale` => `en`
   (p.30)

3. The directory location of composer can be found using the following command:\
   `composer global about`

4. Artisan is the powerful Command-Line Interface (CLI) included with Laravel.

5. Types of Routers\
   There are four main types of routers which are extensively used in Laravel:
   - Redirect routes
   - View routes
   - Route list
   - Fallback routes


6. other way to pass a variable to view, by using `with`. e.g.:\
   ```php
   return view(‘welcome’)
               ->with(‘name’, ‘ABC’)
               ->with(‘organization’, ‘ORGNAME’);
   ```


7. what is the difference between `View::share` and `View:composer` ?\

   in `View::share` we share specific data to all views but\
   in `View::composer` the data is shared among specific view; in other word, we could specify the data should be pass to which view.


8. redirecting to named routes:\
   `return redirect()->route('dashboard', ['id'=>1]);`

9. redirect to specific url:\
   
   ```php
   Route::get(‘/aboutMe’, function () {
      return redirect(‘/home/aboutMe’);
   });
   ```

10. you can also use `return back();` to redirect to previous url. please note that `back()` helper function works based on sessions in laravel. so be careful to use routes which are in `web.php` file because by default session middle is active on web routes. (p.85)\

and also I saw this piece of code on laracast which says all of these methods are same:

```php
return back();

return redirect()->back();

return redirect()->previous();
```
    

11. it is possible to redirect to specific action of a controller and also pass variable to it like so:\

```php
return redirect()->action(
   [EmployeeController::class, ‘dashboard’], [‘id’ => 1]
);
```


12. ypu can create `custom if statement` in laravel balde template engine. how? 😊 

step 1: define your custom if statement in AppServiceProvider

```php
use Illuminate\Support\Facades\Blade;

class AppServiceProvider extends ServiceProvider
{
    // code commented for brevity

    public function boot()
    {
        Blade::if('booktype', function ($booktype) {
            if (in_array($booktype, ['fiction', 'nonfiction'])) {
                return true;
            } 

            return false;
        });
    }
}
```

step 2: then use it

```php
@booktype('fiction')
    // This is a fiction book
@elsebooktype('nonfiction')
    // This is a non-fiction book
@else
    // This book falls into some other category
@endbooktype


// or


@unlessbooktype('nonfiction')
    // This is a non-fiction book
@endbooktype
```


13. in addition of `@foreach` loop, we also have `@forelse` loop in laravel, which is almost like @foreach loop except that it checks if the given array is empty or not. like this:\

```php
@forelse ($employees as $employee)
   <li>{{ $employee->name }}</li>
@empty
   <p>No employees</p>
@endforelse
```


14.  The continuation or break condition may also be included in the directive declaration:

```php
@foreach ($employees as $employee)
   @continue($employee->type == 1)
   <li>{{ $employee->name }}</li>
   @break($employee->number == 5)
@endforeach
```


--------------- Eloquent ---------------


15. If you would like to perform model operations without the model having its updated_at timestamp modified, you may operate on the model within a closure given to the withoutTimestamps method:

```
Model::withoutTimestamps(fn () => $post->increment(['reads']));
```
