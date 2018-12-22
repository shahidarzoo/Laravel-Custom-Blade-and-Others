# Laravel-Custom-Blade, Factroy and Seeds

### Count Grater value and check if it is divisable by any no
```
$status_order = DB::table('shipments')
	->select('shipment_status_id', DB::raw('count(shipment_status_id) as count_status_id'))
	->groupBy('shipment_status_id')
	->where('order_id', 500)
	->get();
$status = array();
$max = 0;
foreach ($status_order as $ship_status) 
{
	if ($ship_status->count_status_id > $max) 
	{
		$max = $ship_status->count_status_id;
	}
}


if($max  % 2 == 0)
{
	echo "Accepted".'<br>';
}

```
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
### Show Pagination in laravel Entries
```php
<div class="dataTables_info" id="example1_info" role="status" aria-live="polite">
          Showing {{($employee->currentpage()-1)*$employee->perpage()+1}} to {{$employee->currentpage()*$employee->perpage()}}
    of  {{$employee->total()}} entries
        </div>

```
