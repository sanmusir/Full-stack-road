## Laravel Excel
#### 要求

- PHP： ^7.0
- Laravel： ^5.5
- PhpSpreadsheet： ^1.6
- PHP扩展已php_zip启用
- PHP扩展已php_xml启用
- PHP扩展已php_gd2启用

#### 安装
 - composer安装  
 composer require maatwebsite/excel  
 ServiceProvider 和 Facade 都是自动发现的，你无需去注册它。

 - 发布配置
 php artisan vendor:publish --provider="Maatwebsite\Excel\ExcelServiceProvider"

#### 基础使用
###### 最简单的使用
- 创建一个导出类
  ```
  使用artisan命令创建，你也可以直接创建
  php artisan make:export UsersExport --model=User

  <?php

  namespace App\Exports;

  use App\User;
  use Maatwebsite\Excel\Concerns\FromCollection;

  class UsersExport implements FromCollection
  {
    public function collection()
    {
        return User::all();
    }
  }
  ```
- 控制器中调用
  ```
  use App\Exports\UsersExport;
  use Maatwebsite\Excel\Facades\Excel;
  use App\Http\Controllers\Controller;

  class UsersController extends Controller
  {
    public function export()
    {
        return Excel::download(new UsersExport, 'users.xlsx');
    }
  }
  ```

###### 自定义输出视图
上述案例只是简单的将数据展示出来，如果我们需要多样化的视图，就需要自定义视图文件

- 创建带视图的导出类
  ```
  namespace App\Exports;

  use App\User;
  use Illuminate\Contracts\View\View;
  use Maatwebsite\Excel\Concerns\FromView;

  class UsersExport implements FromView
  {
      public function view(): View
      {
          return view('exports.users', [
              'users' => User::all()
          ]);
      }
  }
  ```
- 创建视图文件
  ```
  <table>
    <thead>
    <tr>
        <th>用户名</th>
        <th>邮箱</th>
    </tr>
    </thead>
    <tbody>
    @foreach($users as $user)
        <tr>
            <td>{{ $user->name }}</td>
            <td>{{ $user->email }}</td>
        </tr>
    @endforeach
    </tbody>
  </table>
  ```
- 控制器中调用
  ```
  public function export()
  {
    return Excel::download(new InvoicesExport, 'invoices.xlsx');
  }
  ```

###### 同时输出多张表格

- 创建视图
  ```
  <table>
    <thead>
    <tr>
        <th>用户名</th>
        <th>邮箱</th>
    </tr>
    </thead>
    <tbody>
        <tr>
            <td>{{ $user->name }}</td>
            <td>{{ $user->email }}</td>
        </tr>
    </tbody>
  </table>

  ```

- 创建子表
  ```
  <?php

  namespace App\Exports;

  use Illuminate\Contracts\View\View;
  use Maatwebsite\Excel\Concerns\FromView;
  use Maatwebsite\Excel\Concerns\WithTitle;

  class UserSheet implements FromView,WithTitle
  {
    public $user;

    public function __construct($user)
    {
        $this->user = $user;
    }

    //指定子表名称
    public function title(): string
    {
        return '用户' . $this->user->name;
    }

    public function view(): View
    {
        return view('exports.users', [
            'user' => $this->user
        ]);
    }
  }
  ```
- 创建导出类
  ```

  namespace App\Exports;

  use App\User;
  use Maatwebsite\Excel\Concerns\Exportable;
  use Maatwebsite\Excel\Concerns\WithMultipleSheets;

  class UsersExport implements WithMultipleSheets
  {
    use Exportable;

    /**
     * @return array
     */
    public function sheets(): array
    {
        $sheets = [];
        $users  = User::all();

        foreach ($users as $user){
            $sheets[] = new UserSheet($user);
        }
        return $sheets;
    }
  }

  ```
- 控制器调用
  ```
  public function export()
  {
    return Excel::download(new InvoicesExport, 'invoices.xlsx');
  }
  ```

#### 其他

###### 表格自动调整宽度
继承 ShouldAutoSize 接口即可
```
namespace App\Exports;

use Maatwebsite\Excel\Concerns\ShouldAutoSize;

class UsersExport implements ShouldAutoSize
{
    ...
}
```

参考链接  
[laravel Excel](https://docs.laravel-excel.com/3.1/getting-started/)
