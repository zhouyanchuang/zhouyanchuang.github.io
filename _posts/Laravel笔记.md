#### Laravel笔记

##### 安装

`composer create-project --prefer-dist laravel/laravel blog 5.6.*`

##### 代码提示插件

`composer require barryvdh/laravel-ide-helper`

在`config\app.php`文件 providers添加

`Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class,`

在 **app/Providers/AppServiceProvider.php**文件中注册

```
public function register()
{
	if ($this->app->environment() !== 'production') {
		$this->app->register(\Barryvdh\LaravelIdeHelper\IdeHelperServiceProvider::class)
	}
}
```

##### 生成代码跟踪支持

`php artisan ide-helper:generate`

phpstrom打开command line tool(命令) 快捷键 `Ctrl+Shift+x`

##### 低于mysql5.7.7的版本

在**app/Providers/AppServiceProvider.php**中boot()方法中加入

`\Schema::defaultStringLength(191);`

##### 数据填充

`php artisan make:seeder UserSeeder`(填充文件名字)

执行填充

在database/seeds/DatabasesSeeder.php 中的run()方法

```
public function run()
    {
        // $this->call(UsersTableSeeder::class);
        $this->call(UserSeeder::class);
    }
```

写完之后用命令跑一下`artisan db:seed`

##### 模型工厂

使用`php artisan thinker`打开think模式

调用factory()方法进行数据填充

```
factory(App\User::class,10)->make();
factory(App\User::class,10)->create();
```

使用UserSeeder.php run()方法`factory(\App\User::class,10)->create();`

用命令`artisan migrate:refresh --seed`重置并修改第一条数据