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


