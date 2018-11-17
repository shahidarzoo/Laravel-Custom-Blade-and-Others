# Laravel-Custom-Blade-and-Others

##### Inside your App\Providers\AppServiceProvider.php replace boot mathod with following code
```php
use Blade;

public function boot()
{
    Schema::defaultStringLength(191);
    Blade::if('featured', function($post){
        return $post->featured();
    });
}
```
##### Inside your Model create method name like featured()
```php
public function featured()
{
  $post = $this->featured;
  if($post == 'Yes')
  {
    return $post;
  }

}
```
##### Inside your view just use like
```php
@featured($post)  
  <span class="badge badge-primary">Featured</span>
@endfeatured
```
