## 注意
* 此规范为强制规范，必须遵守。
* 代码格式推荐使用[PHP-CS-Fixer](https://cs.symfony.com/)来格式化。
* 文件参考“[PSR-1基本代码规范](http://www.php-fig.org/psr/psr-1/)”。这里有[中文版](https://www.twle.cn/l/yufei/phppsr/php-psr-index.html)。


## PHP代码文件 必须以 <?php 标签开始
纯PHP代码文件，**必须** 省略文件最后的 `?>`

## PHP代码文件必须以 不带BOM的 UTF-8 编码

## 命名空间和类
注：此处的“类”指代所有的类、接口以及可复用代码块（traits）

### 命名空间以及类必须符合 PSR 的自动加载规范：PSR-0 或 PSR-4 中的一个
* 每个类都独立为一个文件
* 命名空间至少有一个层次：顶级的组织名称（vendor name）。比如：
	* namespace Vendor;
	* namespace Vendor\Model;
* 每个 namespace 命名空间声明语句和 use 声明语句块后面，**必须** 插入一个空白行
* 类的属性和方法 **必须** 添加访问修饰符（`private`、`protected` 以及 `public`）， `abstract` 以及 `final` **必须** 声明在访问修饰符之前，而 `static` **必须** 声明在访问修饰符之后
* 属性声明 **绝对不能** 使用 `var` 关键字

### 类的命名必须遵循 StudlyCaps 大写开头的驼峰命名规范
* 文件名应该和类名一致，且为小写

### 类的常量、属性和方法
* 类的常量中所有字母都 **必须** 大写，词间以`下划线 (_)`分隔
* 类的属性命名 **可以** 遵循 小写开头的驼峰式 (`$camelCase`) 、大写开头的驼峰式 (`$StudlyCaps`)和下划线分隔式 (`$under_score`)
	* 不做强制要求，但无论遵循哪种命名方式，一个项目 **应该** 使用一种方式
	* **推荐** 优先使用 小写开头的驼峰式 (`$camelCase`)
* 方法名称 必须 遵循 小写开头的驼峰式 (`$camelCase`)
* 变量名称 可以 遵循 小写开头的驼峰式 (`$camelCase`) 和下划线分隔式 (`$under_score`)
	* 不做强制要求，但无论遵循哪种命名方式，一个项目 **应该** 使用一种方式
	* **推荐** 优先使用 小写开头的驼峰式 (`$camelCase`)
* PHP所有 `关键字` **必须** 全部小写
* 常量 `true` 、`false` 和 `null` **必须** 全部小写
* 不要使用`下划线 (_)`作为前缀，来区分属性是 `protected` 或 `private`
	* 注：以前遗留代码可以慢慢优化，新代码按照此规范执行
* 有默认值的参数，**必须** 放到参数列表的末尾


```php
<?php
namespace Vendor\Model;

use FooInterface;
use BarClass as Bar;
use OtherVendor\OtherPackage\BazClass;

class Foo extends Bar implements FooInterface
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';


    private $camelCase;
    public $UserService;


    final public static function fooBar(int $x, string $y = '')
    {
        if (false) {
            throw new Exception($y);
        }

        return false;
    }
}
```

## 其他规范

* 方法名的命名规则，**应该** 是动词 `set()` 或者动词加名词 `setName()`
* 常量、属性和变量名的命名规则，**应该** 是名词 `$name`
* 非二义性(0和1)的枚举值，**必须** 定义常量或者类属性来识别
* 比如订单状态有6种，切不可以处理时，直接写数字1~6
* 注释内容开始前 **必须** 有一个空格
* 包括行注释和块注释
* 方法的长度(行数)，通常不超过显示器的一屏。如果超出，**应该** 重构为多个方法
* 方法参数不宜过多，如果多的话，比如6、7个时，**应该** 考虑传入数组或者对象的方式进行重构
* **应该** 添加一些空白行来提高代码可读性和标识相关的代码块
* 不建议使用 `$a = $b = 0;` 的声明方式，每个语句不能有多于一个的声明

## 注释
* 类、方法、常量和类属性，**必须** 添加注释
* 变量，根据需要添加注释


```php
<?php

/*
 * This file is part of the XXXXX package.
 *
 * For the full copyright and license information, please view the LICENSE
 * file that was distributed with this source code.
 */

namespace App\Controller\Api;

use App\Service\Api\MemberService;

/**
 * 首页控制器
 * 
 * @author xxxxxx
 * @author yyyyyy
 * 
 */
class Index extends ApiBaseController  implements ControllerInterface
{
    // 缺省用户ID
    const DEFAULT_USER_ID = 123;

    /**
     * @var bool 不要登录验证
     */
    protected $needSignin = false;

    /**
     * 某个月过生日的客户
     *
     * @param int $month  月
     * @param int $gender 性别
     *
     * @return array
     */
    public function monthBirthday(int $month, int $gender = 0)
    {
       // xxx
       $users = [];

       return [];
    }
}
```

## 使用 PHP-CS-Fixer 格式化代码

PHP-CS-Fixer，[PHP Coding Standards Fixer](https://cs.symfony.com/)

所有可用配置项及参考，请访问：[PHP-CS-Fixer Configurator](https://mlocati.github.io/php-cs-fixer-configurator/)。

### 安装
注：以下操作均在MacOS进行，Windows、Linux略有不同，请自行调整。

```
$ cd /usr/local/bin 
$ wget https://cs.symfony.com/download/php-cs-fixer-v2.phar -O php-cs-fixer
$ chmod +x php-cs-fixer
```
### 代码格式化规则
下载[.php_cs](https://github.com/zgia/manual/blob/master/.php_cs)文件放到项目根目录。为了保证项目中，所有人的代码格式一致，此文件需要添加到git。

注意：

1. `"declare_strict_types" => true`，则会在文件开始处添加：`declare(strict_types=1);`，开启强制严格的类型声明模式（PHP >= 7.0）。上面提供的.php_cs，declare_strict_types已经设置为true，可以根据项目需要，自行修改。
2. `→exclude('FOLDER')`是排除无需格式化的目录，可以根据项目需要，自行修改。

### 格式化代码
如果“`/usr/local/bin/`”已经加到PATH，否则php-cs-fixer需要指定全路径。
 
``` 
$ php-cs-fixer fix --config ./.php_cs FILE_OR_FOLDER
```

### 配置到Visual Studio Code

1. 安装插件：`vscode-php-cs-fixer`
2. 编辑settings.json。用户是全局设置，工作区则针对当前项目。点击“在settings.json中编辑”，会打开settings.json文件。
3. 粘贴下面的内容，并将"`/path/to/file`"改成.php_cs所在目录。

```
"[php]": {
"editor.defaultFormatter": "fterrag.vscode-php-cs-fixer"
},
"vscode-php-cs-fixer.config": "/path/to/file/.php_cs",
"vscode-php-cs-fixer.rules": "",
"vscode-php-cs-fixer.toolPath": "/usr/local/bin/php-cs-fixer",
"vscode-php-cs-fixer.fixOnSave": false
```

4. 代码区域右键，或者快捷键即可格式化代码
5. 也可以配置 `"vscode-php-cs-fixer.fixOnSave": true`，或者删除此行。保存时，vscode会自动格式化 

### 配置到PhpStorm
1. 配置-Tools-External Tools，左下角“+”，输入信息。
2. 配置-Keymap，展开External Tools，找到 php-cs-fixer，右键，Add Keyboard Shortcut，按下组合键即可。
3. 代码区域右键，选择 External Tools菜单，或者快捷键即可格式化代码

EOL.
