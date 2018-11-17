# Laravel-Custom-Blade, Factroy and Seeds

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
## Factory 
##### php artisan make:factory ProductFactory --model=Product
```php
$factory->define(App\Product::class, function (Faker $faker) {
    return [
        'title' => $faker->sentence(),
        'description' => $faker->paragraphs(rand(2,10), true),
        'image' => 'img.png',
        'featured' => $faker->randomElement(['Yes' ,'No']),
    ];
});
```
#####  Inside your seeds\DatabaseSeeder.php
```phppublic function run()
{
    $this->call(UsersTableSeeder::class);
    factory('App\Product',12)->create();
}
```
## Seeds
#####  php artisan make:seeder UsersTableSeeder
```php
$user = \DB::table('users')->insert([
            'name' => 'Super Admin',
            'email' =>'admin@gmail.com',
            'password' => bcrypt('123456'),
        ]);
```
